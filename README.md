// ==UserScript==
// @name         Microsoft Rewards Bot
// @namespace    http://tampermonkey.net/
// @version      1.1
// @description  I will hack microsoft rewards for you!!! You can also do other stuff while it is running.
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==
(function() {

    'use strict';
    if (document.readyState == "complete" || document.readyState == "loaded" || document.readyState == "interactive") {
        clickCards()
    } else {

        document.addEventListener("DOMContentLoaded", function(event) {
            clickCards()
        });
    }
})();
function randomString(length) {
    var result = '';
    var characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    var charactersLength = characters.length;
    for ( var i = 0; i < length; i++ ) {
      result += characters.charAt(Math.floor(Math.random() *
 charactersLength));
   }
   return result;
}

function clickCards(){
    var first = true
    const params = new URLSearchParams(window.location.search)
    if (params.has('searchTab')){
        if (params.get('first') == "true"){
            localStorage.setItem('numSearch', 0);
        }
        var numSearch = localStorage.getItem('numSearch');
        if (numSearch === null){
            numSearch = 0
        }
        localStorage.setItem('numSearch', parseInt(numSearch) + 1);
        console.log(numSearch)
        if (numSearch >= 90){
            close();
        }
        document.location.href = "https://www.bing.com/search?searchTab=true&q=" + randomString(3);
    }
    if (window.location.href === "https://rewards.microsoft.com/"){
        window.open("https://www.bing.com/search?q=abc&searchTab=true&first=true", '_blank').focus();
    }
    if (params.has('rnoreward')){
        setInterval(function(){
            if (document.querySelector(".btOption.b_cards")){
                document.querySelector(".btOption.b_cards").click()
            }
            if (document.getElementById("rqStartQuiz")){
                document.getElementById("rqStartQuiz").click()
            }

            var largeAnswer = document.querySelectorAll(".b_cards")
            if (largeAnswer.length){

                for (let i = 0; i < largeAnswer.length; i++) {
                    if (largeAnswer[i].getAttribute("iscorrectoption") === "True"){
                        largeAnswer[i].click()
                    }
                }
            }

            var smallAnswer = document.querySelectorAll(".rqOption")
            if (smallAnswer.length) {
                for (let i = 0; i < smallAnswer.length; i++) {
                    smallAnswer[i].click()
                }
            }

        }, 500)


    }
    var plus10 = document.querySelectorAll(".mee-icon.mee-icon-AddMedium")
    if (plus10){
      var plus10Length = plus10.length

      for (let i = 0; i < plus10Length; i++) {
          console.log(plus10[i])
          plus10[i].parentNode.parentNode.parentNode.parentNode.click()
      }
    }

}
