<header>

    <div
    class="modal fade"
    id="token-prompt"
    tabindex="-1"
    aria-labelledby="token-prompt-label"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="token-prompt-label">
            Dolby.io Dashboard
          </h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <label for="input-token" class="form-label"
            >Demo Client Access Token:</label
          >
          <input id="input-token" type="text" class="form-control" />
        </div>
        <div class="modal-footer">
          <button type="button" id="btn-token" class="btn btn-primary">
            Authenticate
          </button>
        </div>
      </div>
    </div>
  <!-- </div>
<div class="form">
    <input placeholder="Dolby Secret Token" type="text" id="input-token">
    <button id="btn-token">Authenticate</button>
</div> -->

<div class="status_section">
    <button>Inactive</button>
    <div class="round"></div>
    
</div>
<div>
    <p id="message"></p>
</div>

</header>

<style>
    header {
        padding: 20px;
        background-color: black;
        margin-bottom: 3rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
        box-shadow: 1000px 0px 10px  gray;
    }

    header input {
        width: 300px;
        padding: 10px;
        border-radius: 5px;
    }

    @media (max-width: 700px) {
        header {
            flex-direction: column;
            align-items: unset;
            text-align: center;
        }
        header input  {
            width: 80%;
            border-radius: 20px;
        }
    }


    .form button {
        padding: 10px;
        margin-left: 10px;
        border-radius: 5px;
        background-color: hotpink;
        border: none;
        outline: none;
        color: white;
        cursor: pointer;
        outline: none;
    }

    @media (max-width: 700px) {
        .form button {
            margin-top: 10px;
            border-radius: 20px;
        margin-left: unset;


        }

    }

    .round {
        width: 10px;
        height: 10px;
        background-color: red;
        border-radius: 10px;
        margin-left: 10px;

    }

    .status_section {
        display: flex;
        align-items: center;
    }
</style>