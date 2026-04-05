<div id="title">CNN Flower Classification</div>

<div id="wrapper">
    <div id="panel-left">
        <div class="title">Upload flower image</div>
        <div id="file-upload">
            <span>Drag file here</span>
        </div>
        <button id="predict-btn">Predict</button>
        <div class="row" style:gap="8px">
            <div id="time-taken" class="stat" style:flex="1">Time Taken: 0ms</div>
            <button id="clear-image-btn">Clear</button>
        </div>
    </div>

    <div id="panel-right">
        <div class="title">Result</div>
        <div id="output-area">
            <div id="output-image" style:background-image="url(img/sunflower.jpg)"></div>
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

        <div id="class-list">
            <div class="row" style:gap="12px">
                <div class="inline-title">Classes</div>
                <div class="line"></div>
            </div>

            <div id="class-images">
                <div>
                    <div class="class-image" style:background-image="url(img/sunflower.jpg)"></div>
                    <div class="class-name">Sunflower</div>
                </div>
                <div>
                    <div class="class-image" style:background-image="url(img/daisy.jpg)"></div>
                    <div class="class-name">Daisy</div>
                </div>
                <div>
                    <div class="class-image" style:background-image="url(img/dandelion.jpg)"></div>
                    <div class="class-name">Dandelion</div>
                </div>
                <div>
                    <div class="class-image" style:background-image="url(img/rose.jpg)"></div>
                    <div class="class-name">Rose</div>
                </div>
                <div>
                    <div class="class-image" style:background-image="url(img/tulip.jpg)"></div>
                    <div class="class-name">Tulip</div>
                </div>
            </div>
        </div>
    </div>
</div>

<style>
    #wrapper {
        display: grid;
        grid-template-columns: 1fr 2fr;
        gap: 16px;
        padding: 24px;
        max-width: 1280px;
        margin: 0 auto;
    }

    #title {
        /* padding: 16px 32px; */
        padding: 16px;
        text-align: center;
        background: #4593e1;
        color: white;
        font-size: 28px;
        font-weight: 700;
    }

    #file-upload {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 40px;
        border: 2px dashed #4593e1;
        border-radius: 9px;
        color: #4593e1;
        font-weight: 500;
        flex: 1;
    }

    button {
        display: block;
        border: none;
        border-radius: 9px;
        padding: 12px 24px;
        background: #4593e1;
        color: white;
        font-size: 18px;
    }

    button:hover {
        background: #3a7ac1;
    }

    button:active {
        background: #2e5a8c;
    }

    #predict-btn, #clear-image-btn, .stat {
        margin-top: 10px;
    }

    .stat {
        display: block;
        border-radius: 9px;
        padding: 12px;
        text-align: center;
        background: #1eb337;
        color: white;
        font-size: 18px;
    }

    #panel-left, #panel-right {
        background: white;
        border-radius: 9px;
        padding: 24px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }

    #panel-left {
        display: flex;
        flex-direction: column;
    }

    .title {
        padding: 0 6px 0 6px;
        font-size: 22px;
        margin-bottom: 16px;
        font-weight: 400;
    }

    .subtitle {
        font-size: 18px;
        padding-inline: 6px;
        margin-top: 32px;
        font-weight: 500;
    }

    ul {
        margin-block: 12px;
    }

    li {
        margin-block: 12px;
    }

    li::marker {
        color: #4593e1;
    }

    #panel-left > .title, #panel-right > .title {
        padding: 0 6px 10px 6px;
        border-bottom: 1px solid #4593e1;
        color: #4593e1;
        font-weight: 700;
    }

    .inline-title {
        font-size: 22px;
        padding: 0 6px 4px 6px;
        color: #4593e1;
        font-weight: 700;
    }

    .line {
        border-bottom: 1px solid #4593e1;
        flex: 1;
    }

    #class-predictions {
        flex: 1;
        padding-block: 20px;
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

    #class-list {
        margin-top: 12px;
    }

    .row {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }

    #class-images {
        display: flex;
        gap: 8px;
        margin-top: 8px;
    }

    .class-image {
        width: 150px;
        height: 150px;
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        border: 2px solid #4593e1;
        border-radius: 9px;
    }

    .class-name {
        text-align: center;
        margin-top: 6px;
        color: #4593e1;
        font-weight: 500;
    }
</style>
