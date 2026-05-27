<script>
    const LABELS = ['Daisy', 'Dandelion', 'Rose', 'Sunflower', 'Tulip'];

    let outputImage = $state(null);
    let fileInput = $state(null);
    let draggingText = $state('Drag file here');
    let hasImage = $state(false);
    let files = $state([]);
    let predictedClass = $derived(hasImage ? LABELS[prediction.indexOf(Math.max(...prediction))] : '?');
    let prediction = $state([0, 0, 0, 0, 0]);

    function clickFileInput() {
        fileInput.click();
    }

    function clear() {
        hasImage = false;
        draggingText = 'Drag file here';
        fileInput.reset();
    }

    async function uploadFile() {
        if (files.length == 0)
            return;

        let file = files[0];
        let formData = new FormData();
        formData.append('file', file);

        let res = await fetch('http://localhost:5000/predict', {
            method: 'POST',
            body: formData,
        });

        prediction = await res.json();
        hasImage = true;

        let reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = e => outputImage.src = e.target.result;
    }

    function getPercent(label) {
        let index = {
            daisy: 0,
            dandelion: 1,
            rose: 2,
            sunflower: 3,
            tulip: 4,
        }[label];

        return `${Math.round(100 * prediction[index] * 100) / 100}%`;
    }

    $effect(() => {
        if (files.length > 0)
            draggingText = `File: ${files[0].name}`;
    });
</script>

<div id="title">CNN Flower Classification</div>

<!-- svelte-ignore a11y_click_events_have_key_events -->
<!-- svelte-ignore a11y_no_static_element_interactions -->
<!-- svelte-ignore a11y_missing_attribute -->

<div id="wrapper">
    <div id="panel-left">
        <div class="title">Upload flower image</div>
        <div id="file-upload" role="button" tabindex="0"
            onclick={clickFileInput}
            ondragover={e => {
                e.preventDefault();
                draggingText = 'Drop file to upload...';
            }}
            ondrop={e => {
                e.preventDefault();
                files = e.dataTransfer.files;
            }}
            ondragend={e => {
                draggingText = 'Drag file here';
            }}
        >
            <input bind:this={fileInput} bind:files accept="image/png, image/jpeg" type="file" style="display: none">
            <span>{draggingText}</span>
        </div>
        <button id="predict-btn" onclick={uploadFile}>Predict</button>
        <div class="row" style:gap="8px">
            <div id="time-taken" class="stat" style:flex="1">Time Taken: 0ms</div>
            <button id="clear-image-btn" onclick={clear}>Clear</button>
        </div>
    </div>

    <div id="panel-right">
        <div class="title">Result</div>
        <div id="output-area">
            {#if hasImage}
                <img bind:this={outputImage} id="output-image">
                <!-- <div bind:this={outputImage} id="output-image" style:background-image="url(img/sunflower.jpg)"></div> -->
            {:else}
                <div id="output-image" class="placeholder">
                    <span>?</span>
                </div>
            {/if}
            {#if hasImage}
                <div id="class-predictions">
                    <div class="title">Predicted class: <span id="predicted-class">{predictedClass}</span></div>
                    <div class="subtitle">Class Probabilities:</div>
                    <ul>
                        <li>Daisy: <span id="prob-daisy">{getPercent('daisy')}</span></li>
                        <li>Dandelion: <span id="prob-dandelion">{getPercent('dandelion')}</span></li>
                        <li>Rose: <span id="prob-rose">{getPercent('rose')}</span></li>
                        <li>Sunflower: <span id="prob-sunflower">{getPercent('sunflower')}</span></li>
                        <li>Tulip: <span id="prob-tulip">{getPercent('tulip')}</span></li>
                    </ul>
                </div>
            {:else}
                <div id="class-predictions">
                    <div class="title">Predicted class: ?</div>
                    <div class="subtitle">Class Probabilities:</div>
                    <ul>
                        <li>Daisy: <span id="prob-daisy">?%</span></li>
                        <li>Dandelion: <span id="prob-dandelion">?%</span></li>
                        <li>Rose: <span id="prob-rose">?%</span></li>
                        <li>Sunflower: <span id="prob-sunflower">?%</span></li>
                        <li>Tulip: <span id="prob-tulip">?%</span></li>
                    </ul>
                </div>
            {/if}
        </div>

        <div id="class-list">
            <div class="row" style:gap="12px">
                <div class="inline-title">Classes</div>
                <div class="line"></div>
            </div>

            <div id="class-images">
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
                    <div class="class-image" style:background-image="url(img/sunflower.jpg)"></div>
                    <div class="class-name">Sunflower</div>
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

    #output-image.placeholder {
        width: 300px;
        height: 300px;
        background: lightgrey;
        border: 5px solid #4593e1;
        border-radius: 9px;
        margin: 0 auto;
        display: flex;
        text-align: center;
        align-items: center;
        justify-content: center;
        font-weight: bold;
        font-size: 128px;
    }

    #output-image.placeholder > span {
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
