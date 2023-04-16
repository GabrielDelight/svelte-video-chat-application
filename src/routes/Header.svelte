<header>
  <div
    class="modal fade"
    id="token-prompt"
    tabindex="-1"
    aria-labelledby="token-prompt-label"
    aria-hidden="true"
  >
    <div class="flex_div">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-body">
            <input
              id="input-token"
              type="text"
              class="form-control"
              placeholder="Demo Client Access Token"
            />
          </div>
          
          <div class="modal-footer">
            <button type="button" id="btn-token" class="btn btn-primary">
              Authenticate
            </button>
          </div>
        </div>
      </div>

      <div class="status_section">
        <button id="statusBtn">Inactive</button>
        <div class="round" />
      </div>
    </div>
  </div>
  <div class="error_log">
    <input type="" id="message">
  </div>
</header>

<style>
  header {
    padding: 20px;
    background-color: black;
    margin-bottom: 3rem;
    /* display: flex;
    justify-content: space-between;
    align-items: center; */
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
    header input {
      width: 80%;
      border-radius: 20px;
    }
  }
  .flex_div {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  #token-prompt {
    display: flex;
    /* align-items: center; */
    justify-content: space-between;
    width: 100%;
  }

  .modal-content {
    display: flex;
    align-items: center;
  }

  .modal-content button {
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

  .error_log input {
    margin-top: 10px;
    background-color: #ddd;
    color: black;
    width: 100%;
  }
</style>
