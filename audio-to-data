import { AudioContext } from 'node-web-audio-api';
import fs from "fs";

const audioContext = new AudioContext();

function getFreqs() {

    const analyser = audioContext.createAnalyser();
    let buffer = [];
    try {
        buffer = fs.readFileSync('/Users/surfista/Desktop/capsule-stl-main/media/come-together.mp3');
        // The 'buffer' variable now contains the audio file data as a Buffer
        console.log('Audio file read successfully into buffer:', buffer);
    } catch (err) {
        console.error('Error reading file:', err);
    }

    const nodeBuffer = Buffer.from(buffer);
    const arrayBuffer = nodeBuffer.buffer;

    audioContext.decodeAudioData(arrayBuffer, (audioBuffer) => {
        const source = audioContext.createBufferSource();

        source.buffer = audioBuffer;
        source.connect(analyser);
        // analyser.connect(audioContext.destination);
        // source.start();

        analyser.fftSize = 2048;

        const bufferLength = analyser.frequencyBinCount;
        const dataArray = new Uint8Array(bufferLength);

        // analyser.getByteTimeDomainData(dataArray);
        analyser.getByteFrequencyData(dataArray);

        let counter = 50

        while (counter > 0) {
            console.log(dataArray[counter])
            counter--
        }
    });


}

getFreqs()
