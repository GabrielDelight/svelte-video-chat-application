
<script>
	import  Myheader from "./MyHeader.svelte";
</script>
<Myheader />
<div class="video_container">
	<div class="video_wrapper">

	</div>

	<div class="video_wrapper">

	</div>
</div>

<br>
<div class="footer_container">
		<button>Join</button>
		<button>Leave</button>
		<button>Invite</button>

</div>

<style>
	.video_container {
		width: 80%;
		height: 60vh;
		margin:  auto;	
		display: flex;
		padding: 10px;
		justify-content: space-between;
		
	}

	@media (max-width: 600px) {
		.video_container  {
			flex-direction: column;
			width: 100%;
		}
	}

	.video_wrapper  {
		flex-basis: 45%;
		background-color: rgb(43 47 49);
		border: 10px;
		height: 100%;
		border-radius: 10px;
	}

	

	.footer_container  {
		width: 50%;
		margin: auto;
		background-color: black;
		padding: 10px;
		box-shadow: 8px 9px 10px #d9d9d9;
		border-radius: 10px;
	}

	@media (max-width: 600px) {
		.footer_container  {
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
	}
	
	.footer_container button:nth-child(1)  {
		background-color: green;
	}


	.footer_container button:nth-child(2)  {
		background-color: red;
	}

	.footer_container button:nth-child(3)  {
		background-color: gray;
	}
</style>