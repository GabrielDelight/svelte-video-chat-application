<script>
  import Myheader from "./MyHeader.svelte";
  import { onMount } from "svelte";

  onMount(async () => {
    const shareMessage = (message) => {
      document.getElementById("message").innerText = message;
    };

    // Step 1: Define initializeToken() Here
    const initializeToken = () => {
      const token = dolbyio.getAccessToken();
      VoxeetSDK.initializeToken(
        token,
        () => new Promise((resolve) => resolve(token))
      );

      console.log("===>", token);
      shareMessage("Step 1: Web SDK initialized.");
      return token;
    };

    // Step 2: Define openSession() Here
    const openSession = async (sessionName) => {
      try {
        await VoxeetSDK.session.open({ name: sessionName });
        shareMessage("Step 2: Session opened.");
      } catch (error) {
        shareMessage("Error: Make sure you have a valid Dolby.io Client Token");
      }
    };

    // Step 3: Define createAndJoinConference() Here
    const createAndJoinConference = async (
      conferenceAlias,
      participantName
    ) => {
      if (!VoxeetSDK.session.isOpen()) {
        await openSession(participantName);
      }
      const conferenceOptions = {
        alias: conferenceAlias,
      };
      const joinOptions = {
        constraints: { audio: true, video: true },
      };

      try {
        const conference = await VoxeetSDK.conference.create(conferenceOptions);
        await VoxeetSDK.conference.join(conference, joinOptions);
        shareMessage(
          `Step 3: Conference '${conferenceAlias}' created and joined.`
        );
      } catch (error) {
        console.error(error);
      }
    };

    // Step 4: Define handleConferenceFlow() Here
    const handleConferenceFlow = () => {
      VoxeetSDK.conference.on("streamAdded", (participant, stream) => {
        if (stream.type === "Camera") {
          shareVideo(participant, stream);
        }
      });

      VoxeetSDK.conference.on("streamUpdated", (participant, stream) => {
        if (stream.type === "Camera" && stream.getVideoTracks().length) {
          shareVideo(participant, stream);
        }
      });

      // Step 6: Later in step 6 we will define leave handlers here

      VoxeetSDK.conference.on("streamRemoved", (participant, stream) => {
        const videoNode = document.getElementById(`video-${participant.id}`);
        if (videoNode) {
          videoNode.parentNode.removeChild(videoNode);
        }
      });

      VoxeetSDK.conference.on("left", async () => {
        await VoxeetSDK.session.close();
      });
    };

    // Step 4: Define shareVideo() Here
    const shareVideo = async (participant, stream) => {
      let perspective = "self-view";
      if (VoxeetSDK.session.participant.id !== participant.id) {
        perspective = "remote-view";
      }

      let videoNode = document.getElementById(`video-${participant.id}`);
      if (!videoNode) {
        videoNode = document.createElement("video");

        videoNode.setAttribute("id", `video-${participant.id}`);
        videoNode.setAttribute("height", "100%");
        videoNode.setAttribute("width", "100%");

        videoNode.muted = true;
        videoNode.autoplay = true;
        videoNode.playsinline = true;

        console.log(videoNode);

        const videoContainer = document.getElementById(perspective);
        videoContainer.lastElementChild.replaceWith(videoNode);
        videoContainer.firstElementChild.innerText = participant.info.name;
      }

      navigator.attachMediaStream(videoNode, stream);
      shareMessage(
        `Step 4: Video of participant '${participant.info.name}' started.`
      );
    };

    // Step 6: Define leaveConference() Here

    const leaveConference = async () => {
      try {
        await VoxeetSDK.conference.leave();
        shareMessage("Getting Started: Conference has ended.");
      } catch (error) {
        console.error(error);
      }
    };

    const main = async () => {
      // Configure the application from query parameter values
      const queryParams = new URLSearchParams(window.location.search);
      const name = queryParams.get("name") || "developer";
      const alias = queryParams.get("alias") || "web-sdk-starter";

      // Step 1: Call initializeToken() Here
      const token = await initializeToken();
      // Step 2: Call openSession() Here
      await openSession(name);

      // Step 3: Call createAndJoinConference() Here
      document.getElementById("btn-join").onclick = async () => {
        await createAndJoinConference(alias, name);
      };

      // Step 4: Call handleConferenceFlow() Here
      handleConferenceFlow();

      // Step 5: Create Invite link Here
      document.getElementById("btn-invite").onclick = () => {
        const url = `https://developer.dolby.io/demos/comms-sdk-web-getting-started/index.html?token=${token}&alias=${alias}&name=guest`;
        navigator.clipboard.writeText(url);
        shareMessage(`Share the URL copied to your browser clipboard: ${url}`);
      };

      // Step 6: Call leaveConference() Here
      document.getElementById("btn-leave").onclick = async () => {
        await leaveConference();
      };
    };

    main();
  });
</script>

<svelte:head>
  <script
    type="text/javascript"
    src="https://cdn.jsdelivr.net/npm/@voxeet/voxeet-web-sdk/dist/voxeet-sdk.js"
  ></script>
  <script
    type="text/javascript"
    src="https://developer.dolby.io/demos/comms-sdk-web-getting-started/util/dolbyio-auth-helper.js"
  ></script>

  <script
    src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"
    integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p"
    crossorigin="anonymous"
  ></script>
</svelte:head>

<Myheader />

<div class="video_container">
  <div class="video_wrapper">
    <div id="self-view">
      <!-- Container for the local participant media stream -->
      <p id="self-view-username" />
      <i class="display-1 bi bi-person-video position-relative" />
    </div>
  </div>

  <div class="video_wrapper">
    <div id="remote-view">
      <!-- Container for the remote participant media stream -->
      <p id="remote-view-username" />
      <i class="display-1 bi bi-person-video position-relative" />
    </div>
  </div>
</div>

<br />
<div class="footer_container">
  <button id="btn-join">Join</button>
  <button id="btn-leave">Leave</button>
  <button id="btn-invite">Invite</button>
</div>

<style>

  .video_container {
    width: 80%;
    height: 60vh;
    margin: auto;
    display: flex;
    padding: 10px;
    justify-content: space-between;
  }

  @media (max-width: 600px) {
    .video_container {
      flex-direction: column;
      width: 100%;
    }
  }

  .video_wrapper {
    flex-basis: 45%;
    background-color: rgb(43 47 49);
    border: 10px;
    height: 100%;
    border-radius: 10px;
  }

  .footer_container {
    width: 30%;
    margin: auto;
    background-color: black;
    padding: 10px;
    box-shadow: 1px 2px 10px #525252;
    border-radius: 10px;
    display: flex;
    justify-content: space-between;
  }

  @media (max-width: 600px) {
    .footer_container {
      width: 90%;
      margin: auto;
    }
  }

  .footer_container button {
    padding: 10px 20px;
    margin-right: 10px;
    cursor: pointer;
    color: white;
    border-radius: 5px;
    border: none;
    cursor: pointer;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 13px;
    text-align: center;
  }

  .footer_container button:nth-child(1) {
    background-color: green;
  }

  .footer_container button:nth-child(2) {
    background-color: red;
  }

  .footer_container button:nth-child(3) {
    background-color: gray;
  }



</style>
