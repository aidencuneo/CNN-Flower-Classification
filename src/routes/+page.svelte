<div id="title">CNN Flower Classification</div>

<div id="wrapper">
    <div id="panel-left">
        <div class="title">Upload flower image</div>
        <file-upload>Drag file here</file-upload>
        <button>Predict</button>
    </div>

    <div id="panel-right">
        <div class="title">Result</div>
        <div id="output-area">
            <div id="output-image" style:background-image="url(sunflower.jpg)"></div>
            <div id="class-predictions">
                <div class="title">Predicted class: <span id="predicted-class">Sunflower</span></div>
                <div class="subtitle">Class Probabilities:</div>
                <ul>
                    <li>Sunflower: <span id="prob-sunflower">90%</span></li>
                    <li>Daisy: <span id="prob-daisy">3%</span></li>
                    <li>Dandelion: <span id="prob-dandelion">2.5%</span></li>
                    <li>Rose: <span id="prob-rose">2.5%</span></li>
                    <li>Tulip: <span id="prob-tulip">2%</span></li>
                </ul>
            </div>
        </div>
    </div>
</div>

<style>
    #title {
        /* padding: 16px 32px; */
        padding: 16px;
        text-align: center;
        background: #4593e1;
        color: white;
        font-size: 28px;
        font-weight: 700;
    }

    #wrapper {
        display: grid;
        grid-template-columns: 1fr 2fr;
        gap: 16px;
        padding: 24px;
        max-width: 1280px;
        margin: 0 auto;
    }

    #panel-left, #panel-right {
        background: white;
        border-radius: 9px;
        padding: 24px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }

    .title {
        font-size: 22px;
        padding: 0 6px 10px 6px;
        border-bottom: 1px solid #4593e1;
        margin-bottom: 16px;
        font-weight: 400;
    }

    .subtitle {
        font-size: 18px;
        padding-inline: 6px;
    }

    ul {
        /* color: #4593e1; */
    }

    li {
        margin-block: 12px;
    }

    li::marker {
        color: #4593e1;
    }

    #panel-left > .title, #panel-right > .title {
        color: #4593e1;
        font-weight: 700;
    }

    #class-predictions {
        flex: 1;
        padding-block: 16px;
    }

    #predicted-class {
        color: #4593e1;
        font-weight: 700;
    }

    #output-area {
        display: flex;
        gap: 16px;
    }

    #output-image {
        width: 300px;
        height: 300px;
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        border: 5px solid #4593e1;
        border-radius: 9px;
        /* margin: 16px; */
    }

    #prob-sunflower,
    #prob-daisy,
    #prob-dandelion,
    #prob-rose,
    #prob-tulip {
        color: #4593e1;
        font-weight: 700;
    }
</style>
