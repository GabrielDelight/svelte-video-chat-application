<header>
<div class="form">
    <input placeholder="Dolby Secret Token" type="text">
    <button>Authenticate</button>
</div>

<div class="status_section">
    <button>Inactive</button>
    <div class="round"></div>
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