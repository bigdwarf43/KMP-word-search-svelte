

  <script>
    import { set_data } from "svelte/internal";


    let pat = ''
    let loc = null
    let randomSent = ''

  async function getSentence() {
    randomSent =  " ";
    for(var i=0; i<10; i++){
      const x = await fetch ('https://cognitivestimulation.tech/api/sentence/getsentence10');
      const y = await x.json();
      randomSent +=  y[0]+". ";
    }
    
  }

  getSentence()


    var makeKMPTable = function(word) {
    if(Object.prototype.toString.call(word) == '[object String]' ) {
        word = word.split('');
    }
    var results = [];
    var pos = 2;
    var cnd = 0;

    results[0] = -1;
    results[1] = 0;
    while (pos < word.length) {
        if (word[pos - 1] == word[cnd]) {
            cnd++;
            results[pos] = cnd;
            pos++;
        } else if (cnd > 0) {
            cnd = results[cnd];
        } else {
            results[pos] = 0;
            pos++;
        }
    }
    return results;
};

var KMPSearch = function(string, word) {
    if(Object.prototype.toString.call(string) == '[object String]' ) {
        string = string.split('');
    }
    if(Object.prototype.toString.call(word) == '[object String]' ) {
        word = word.split('');
    }

    var index = -1;
    var m = 0;
    var i = 0;
    var T = makeKMPTable(word);

    while (m + i < string.length) {
        if (word[i] == string[m + i]) {
            if (i == word.length - 1) {
                return m;
            }
            i++;
        } else {
            m = m + i - T[i];
            if (T[i] > -1) {
                i = T[i];
            } else {
                i = 0;
            }
        }
    }
    return index;
};

    $:{
      loc = KMPSearch(randomSent, pat);
    } 
    </script>

<div class="main-menu">
    <div class="container">
      <h1>Word search</h1>
      <input class="input-field" bind:value={pat}> 
    
      {#if loc==-1}
      <h2>index: not found</h2>
      {:else}
      <h2>index: {loc}</h2>
      {/if}
 
      <button class="button" on:click={getSentence}>Get new para</button>
      <br><br>
   
      {#each randomSent.split("") as part, i}
        <span class={i < loc+pat.length  && i >= loc && loc!=-1? "highlight" : "para"}>{part}</span>
      {/each}


    </div>
</div>


<style>
* {
  box-sizing: border-box;
  overflow: hidden
}

.highlight {
    border-bottom: 3px solid red;
    color: red;
  }

.highlight,
.para {
  font-size: 2rem;
}

.main-menu {
  display: grid;
  position: fixed;
  height: 100vh;
  width: 100%;
  top: 0;
  left: 0;
  background: #0d3b66;
  color: #fff;
  font-family: "Roboto", sans-serif;
  text-align: center;
  place-items: center;
}


.container {
  padding: 0 32px;
}

.main-menu h1 {
  font-size: 70px;
  margin: 8px 0;
}


.button {
  background-color: #4CAF50; 
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
}

.button:hover{
  background-color: #188d20; 
}

.input-field{
  width: 30%;
  border: 0;
  border-bottom: 2px solid gray;
  outline: 0;
  font-size: 2rem;
  color: white;
  padding: 7px 0;
  background: transparent;
  text-align: center;
        }

  </style>

  
