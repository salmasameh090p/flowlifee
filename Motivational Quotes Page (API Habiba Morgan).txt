function loadQuote() {
    fetch("https://api.adviceslip.com/advice")
        .then(response => response.json())
        .then(data => {
            document.getElementById("quote").innerText =
                `"${data.slip.advice}"`;
        })
        .catch(() => {
            document.getElementById("quote").innerText =
                "stay positive and keep going.";
        });
}

// load quote on page open
loadQuote();

// load new quote on button click
document
    .getElementById("new-quote-btn")
    .addEventListener("click", loadQuote);
