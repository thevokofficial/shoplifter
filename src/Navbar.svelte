<script>
    export let selected = ""
    export let isCartVisible = false
    function changeSelected(value) {
        selected = value
    }
</script>

<div class="navbar">
    <img on:click={()=>{
        isCartVisible = !isCartVisible
    }}
    src="icons/ikonka.png"
    alt="icon"
    width="100px"
    height="100px"
    >

    <h1>SHOP LIFTER</h1>

    <div class="navbar-buttons">
        <button type="button" on:click={()=>{changeSelected("")}}>Všechny produkty</button>
        <button type="button" on:click={()=>{changeSelected("gaming")}}>Gaming</button>
        <button type="button" on:click={()=>{changeSelected("mobil")}}>Mobilní telefony</button>
        <button type="button" on:click={()=>{changeSelected("pc")}}>Počítače</button>
    </div>
</div>

<style>
	h1 {
		color: #303633;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 700;
        margin-bottom: 5rem;
	}

    .navbar {
        width: 50vw;
        margin: 0 auto;
        margin-bottom: 5rem;
        text-align: center;
    }

    .navbar-buttons {
        display: flex;
        justify-content: space-around;
    }

    .navbar img:hover{
        cursor: pointer;
    }

    button {
        outline: none;
        border: none;
        color: #ffffff;
        font-size: 20px;
        padding: 15px 25px;
        background-color: #A790A5;
        cursor: pointer;
        box-shadow: 2px 2px 0 #30363310;
        border-radius: 8px;
    }

    button:hover {
        background-color: #ffffff;
        color: #A790A5; 
    }

    button:active {
        box-shadow: 0 1px #303633;
        transform: translateY(4px);
    }
</style>