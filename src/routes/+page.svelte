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
            <div id="output-image"></div>
            <div>
                <div class="title">Predicted Class:</div>
                <div>Class Probabilities:</div>
                <ul>
                    <li>Sunflower:</li>
                    <li>Daisy:</li>
                    <li>Dandelion:</li>
                    <li>Rose:</li>
                    <li>Tulip:</li>
                </ul>
            </div>
        </div>
    </div>
</div>

<style>
    #title {
        padding: 16px 32px;
        background: #4593e1;
        color: white;
        font-size: 24px;
        font-weight: 700;
    }

    #wrapper {
        display: grid;
        grid-template-columns: 1fr 2fr;
        gap: 16px;
        padding: 24px;
    }

    #panel-left, #panel-right {
        background: white;
        border-radius: 9px;
        padding: 16px;
    }

    #panel-left > .title, #panel-right > .title {
        font-size: 20px;
        color: #4593e1;
        font-weight: 700;
        padding: 0 6px 8px 6px;
        border-bottom: 1px solid #4593e1;
    }

    #output-area {
        display: flex;
    }

    #output-area > .title {

    }
</style>
