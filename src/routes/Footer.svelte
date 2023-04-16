<footer>
    <div class="footer_container">
        <button id="btn-join">Join</button>
        <button id="btn-leave">Leave</button>
        <button id="btn-invite">Invite</button>
      </div>
</footer>

<style>
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
