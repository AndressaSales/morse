<script setup>
const Code =({
  A: ".-",
  B: "-...",
  C: "-.-.",
  D: "-..",
  E: ".",
  F: "..-.",
  G: "--.",
  H: "....",
  I: "..",
  J: ".---",
  K: "-.-",
  L: ".-..",
  M: "--",
  N: "-.",
  O: "---",
  P: ".--.",
  Q: "--.-",
  R: ".-.",
  S: "...",
  T: "-",
  U: "..-",
  V: "...-",
  W: ".--",
  X: "-..-",
  Y: "-.--",
  Z: "--..",
  0: "-----",
  1: ".----",
  2: "..---",
  3: "...--",
  4: "....-",
  5: ".....",
  6: "-....",
  7: "--...",
  8: "---..",
  9: "----.",
  ".": ".-.-.-",
  ",": "--..--",
  "?": "..--..",
  "'": ".----.",
  "!": "-.-.--",
  "/": "-..-.",
  "(": "-.--.",
  ")": "-.--.-",
  "&": ".-...",
  ":": "---...",
  ";": "-.-.-.",
  "=": "-...-",
  "+": ".-.-.",
  "-": "-....-",
  _: "..--.-",
  '"': ".-..-.",
  $: "...-..-",
  "@": ".--.-.",
  " ": "/",
});

const reverse = {};
for (const key in Code) {
  if (Code.hasOwnProperty(key)) {
    const value = Code[key];
    reverse[value] = key;
  }
}

const traduz=(()=>{

   
const input = document.getElementById("input");
const traducao = document.getElementById("traducao");

    const inputText = input.value.trim().toUpperCase();
  if (input === "") {
    traducao.textContent = "No Input Provided";
    return;
  }
  if (inputText.includes(".")) {
    const morseWords = inputText.split("/");
    const translatedWords = morseWords.map((morseWord) => {
      const morseChars = morseWord.split(" ");
      return morseChars
        .map((morseChar) => {
          return reverse[morseChar] || morseChar;
        })
        .join("");
    });
    traducao.textContent = translatedWords.join(" ");
  } else {
    const p = inputText.split(" ");
    const traducaoPalavras = p.map((palavra) => {
      const caracteres = palavra.split("");
      const morse = caracteres.map((char) => {
        return Code[char] || char;
      });
      return morse.join(" ");
    });
    traducao.textContent = traducaoPalavras.join("/");
  }
})
</script>


<template>
    <div class="justify-center items-center flex flex-col">
       <div>
            <label class="text-xl pl-2 border-l-stone-600 border-2 pr-18 text-base lg:text-2xl" for="input">
                Digite texto ou código Morse:
            </label>
            <UTextarea color="sky" id="input" rows="4" class="py-5" placeholder="Escreva...." />
       </div>

       <div>
        <UButton class="w-48" @click="traduz" color="sky"><p class="text-center pl-14 font-bold">Traduzir</p></UButton>
       </div>
       <p class="font-bold flex flex-col p-3 pr-52 lg:text-2xl">Tradução: <span class="font-normal" id="traducao"></span></p>
    </div>
</template>