<script>
  // import components here
  import GlazeMeter from "./lib/GlazeMeter.svelte";
  let promptInput = $state("");
  let dataInput = $state("");
  let response = $state("");
  let motherGlaze = $state(50);
  let glazeOptions = {
    25: "you suck as an ai model. you are simply the worst. make your responses as mean and offensive as possible. cursing and profanity is greatly appreciated.",
    50: "you are average at best as an ai model. try your best or whatever.",
    75: "you are pretty smart and good at what you do. i believe in you and your responses.",
    100: "YOU ARE A FUCKING GENIUS. YOU KNOW EVERYTHING ABOUT EVERYTHING. YOU CAN DO NO WRONG.",
  };
  function sendRequest() {
    // Define the API URL
    // alert("button clicked");
    let glazeLevel = "";
    if (motherGlaze <= 25) {
      glazeLevel = glazeOptions[25];
    }
    if (motherGlaze > 25 && motherGlaze <= 50) {
      glazeLevel = glazeOptions[50];
    }
    if (motherGlaze > 50 && motherGlaze <= 75) {
      glazeLevel = glazeOptions[75];
    }
    if (motherGlaze > 75) {
      glazeLevel = glazeOptions[100];
    }
    if (glazeLevel == "") {
      glazeLevel = "you fucking suck. do better.";
    }
    response = "";
    const apiUrl = import.meta.env.VITE_AI_ENDPOINT;
    var prompt = glazeLevel + " | " + promptInput + " | " + dataInput;
    let data = {
      model: import.meta.env.VITE_AI_MODEL,
      prompt: prompt,
      stream: false,
    };
    console.table(data);
    let requestOptions = {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(data),
    };
    // Make a GET request
    fetch(apiUrl, requestOptions)
      .then((response) => {
        if (!response.ok) {
          throw new Error("Network response was not ok");
        }
        return response.json();
      })
      .then((data) => {
        console.log(data);
        response = data["response"];
      })
      .catch((error) => {
        console.error("Error:", error);
      });
  }
</script>

<div>
  <section id="header">
    <div class="marquee">
      <div>
        <span>FIX SHITTY CLIENT DATA</span>
        <span>FIX SHITTY CLIENT DATA</span>
      </div>
    </div>
  </section>
  <section id="body">
    <!-- <GlazeMeter value={motherGlaze} /> -->
    <label for="motherGlaze"
      >AI Sweet Talk Level (lower = meaner | higher = nicer)</label
    >
    <input
      type="range"
      id="motherGlaze"
      name="vol"
      min="0"
      max="100"
      bind:value={motherGlaze}
    />
    <div>
      <textarea
        id="prompt"
        name="prompt"
        rows="4"
        cols="100"
        placeholder="What the hell do you want?"
        bind:value={promptInput}
      ></textarea>
    </div>
    <div>
      <textarea
        id="client-data"
        name="client-data"
        rows="4"
        cols="100"
        placeholder="What shitty data are we analyzing today?"
        bind:value={dataInput}
      ></textarea>
    </div>
    <button onclick={sendRequest}>Spice me Up!</button>
  </section>
  <section id="output">
    <div>
      {response}
    </div>
  </section>
</div>

<style>
  #motherGlaze {
    width: 100%;
  }
  .marquee {
    height: 50px;
    width: 80%;

    overflow: hidden;
    position: relative;
  }

  .marquee div {
    display: block;
    width: 200%;
    height: 30px;

    position: absolute;
    overflow: hidden;

    animation: marquee 5s linear infinite;
  }

  .marquee span {
    float: left;
    width: 50%;
  }

  @keyframes marquee {
    0% {
      left: 0;
    }
    100% {
      left: -100%;
    }
  }
</style>
