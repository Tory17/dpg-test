<script>
  import Button from "./lib/Button.svelte";

  let src = "/src/assets/back1.png";
  let x = "";
  let y = "";
  let operation = "";

  function handler() {
    document.addEventListener("keydown", function (event) {
      if (
        (event.keyCode > 47 && event.keyCode < 58 && event.shiftKey == false) ||
        (event.keyCode > 95 && event.keyCode < 106) ||
        event.keyCode == 110 ||
        event.keyCode == 191 ||
        event.keyCode == 190
      ) {
        x += event.key;
      }
      if (
        (event.keyCode == 187 && event.shiftKey == false) ||
        event.keyCode == 13
      )
        result();
      if (
        event.keyCode == 106 ||
        event.keyCode == 107 ||
        event.keyCode == 111 ||
        event.keyCode == 109 ||
        ((event.keyCode == 187 ||
          event.keyCode == 56 ||
          event.keyCode == 191) &&
          event.shiftKey == true) ||
        (event.keyCode == 189 && event.shiftKey == false)
      ) {
        operation = event.key;
        action(operation);
      }
      if (event.keyCode == 8) back();
      if (event.keyCode == 46) clear();
      if (event.keyCode == 53 && event.shiftKey == true) prosent();
    });
  }
  handler();
  function enterNumber(num) {
    if (x.length > 10) {
      return;
    }

    x += `${num}`;
  }

  function back() {
    x = x.substring(0, x.length - 1);
  }
  function clear() {
    x = "";
    y = "";
    operation = "";
  }
  function prosent() {
    if (y != "") {
      x = (+y * +x) / 100;
    } else {
      x = +x / 100;
    }
  }
  function pl() {
    x = -1 * +x;
  }
  function action(arg) {
    // result();
    y = "";
    y = x;
    operation = arg;
    x = "";

    console.log(`x:${x}, y:${y} , op:${operation}`);
  }
  function result() {
    switch (operation) {
      case "+":
        x = +x + +y;
        console.log(`x:${x}, y:${y} , op:${operation}`);

        break;
      case "-":
        x = +y - +x;
        console.log(`x:${x}, y:${y} , op:${operation}`);

        break;
      case "*":
        x = +y * +x;
        console.log(`x:${x}, y:${y} , op:${operation}`);

        break;
      case "/":
        x = +y / +x;
        console.log(`x:${x}, y:${y} , op:${operation}`);

        break;
    }
  }
</script>

<main>
  <section>
    <div class="container">
      <div class="input">{x}</div>
      <Button on:click={clear}>AC</Button>
      <Button on:click={prosent}>&#x25;</Button>
      <Button on:click={pl}>&plusmn;</Button>
      <Button on:click={back} btn><img {src} alt=" " /></Button>
      <Button on:click={() => enterNumber(7)}>7</Button>
      <Button on:click={() => enterNumber(8)}>8</Button>
      <Button on:click={() => enterNumber(9)}>9</Button>
      <Button on:click={() => action("/")} btn>&divide;</Button>
      <Button on:click={() => enterNumber(4)}>4</Button>
      <Button on:click={() => enterNumber(5)}>5</Button>
      <Button on:click={() => enterNumber(6)}>6</Button>
      <Button on:click={() => action("*")} btn>x</Button>
      <Button on:click={() => enterNumber(1)}>1</Button>
      <Button on:click={() => enterNumber(2)}>2</Button>
      <Button on:click={() => enterNumber(3)}>3</Button>
      <Button on:click={() => action("-")} btn>-</Button>
      <Button on:click={() => enterNumber(".")}>,</Button>
      <Button on:click={() => enterNumber(0)}>0</Button>
      <Button on:click={result}>=</Button>
      <Button on:click={() => action("+")} btn>+</Button>
    </div>
  </section>
</main>

<style>
  .container {
    padding: 30px 15px;
    width: 300px;
    background-color: #f1f1f3;
    max-width: 300px;
    border-radius: 5%;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    font-family: "Courier New", Courier, monospace;
    font-weight: 600;
    font-size: 20px;
  }
  .input {
    width: 100%;
    background: transparent;
    border: none;
    color: #ff9e0e;
    min-height: 150px;
    outline: none;
    grid-column: 1/-1;
    font-size: 40px;
    display: flex;
    justify-content: end;
    align-items: center;
    line-height: 1em;
    word-break: break-all;
    word-wrap: break-word;
  }
</style>
