# Text-to-speech Python\* Demo

## Description
The text to speech demo show how to run the ForwardTacotron and WaveRNN models or modified ForwardTacotron and MelGAN models to produce an audio file for a given input text file.
The demo is based on https://github.com/seungwonpark/melgan, https://github.com/as-ideas/ForwardTacotron and https://github.com/fatchord/WaveRNN repositories.

## How It Works

Upon the start-up, the demo application reads command-line parameters and loads four or three networks to the
Inference Engine plugin. The demo pipeline reads text file by lines and divides every line to parts by punctuation marks.
The heuristic algorithm chooses punctuation near to the some threshold by sentence length.
When inference is done, the application outputs the audio to the WAV file with 22050 Hz sample rate.

## Running

Running the application with the `-h` option yields the following usage message:

```
usage: text_to_speech_demo.py [-h] -m_duration MODEL_DURATION -m_forward
                              MODEL_FORWARD -i INPUT [-o OUT] [-d DEVICE]
                              [-m_upsample MODEL_UPSAMPLE] [-m_rnn MODEL_RNN]
                              [--upsampler_width UPSAMPLER_WIDTH]
                              [-m_melgan MODEL_MELGAN]

Options:
  -h, --help            Show this help message and exit.
  -m_duration MODEL_DURATION, --model_duration MODEL_DURATION
                        Required. Path to ForwardTacotron`s duration
                        prediction part (*.xml format).
  -m_forward MODEL_FORWARD, --model_forward MODEL_FORWARD
                        Required. Path to ForwardTacotron`s mel-spectrogram
                        regression part (*.xml format).
  -i INPUT, --input INPUT
                        Text file with text.
  -o OUT, --out OUT     Required. Path to an output .wav file
  -d DEVICE, --device DEVICE
                        Optional. Specify the target device to infer on; CPU,
                        GPU, FPGA, HDDL, MYRIAD or HETERO is acceptable. The
                        sample will look for a suitable plugin for device
                        specified. Default value is CPU
  -m_upsample MODEL_UPSAMPLE, --model_upsample MODEL_UPSAMPLE
                        Path to WaveRNN`s part for mel-spectrogram upsampling
                        by time axis (*.xml format).
  -m_rnn MODEL_RNN, --model_rnn MODEL_RNN
                        Path to WaveRNN`s part for waveform autoregression
                        (*.xml format).
  --upsampler_width UPSAMPLER_WIDTH
                        Width for reshaping of the model_upsample in WaveRNN
                        vocoder. If -1 then no reshape. Do not use with FP16
                        model.
  -m_melgan MODEL_MELGAN, --model_melgan MODEL_MELGAN
                        Path to model of the MelGAN (*.xml format).
```

Running the application with the empty list of options yields the usage message and an error message.

## Example for running with arguments

### ForwardTacotron with WaveRNN
```
python3 text_to_speech_demo.py \
    --input <path_to_file>/text.txt \
    -o <path_to_audio>/audio.wav \
    --model_duration <path_to_model>/forward_tacotron_duration_prediction.xml \
    --model_forward <path_to_model>/forward_tacotron_regression.xml \
    --model_upsample <path_to_model>/wavernn_upsampler.xml \
    --model_rnn <path_to_model>/wavernn_rnn.xml
```
### Modified ForwardTacotron with MelGAN
```
python3 text_to_speech_demo.py \
    -i <path_to_file>/text.txt \
    -o <path_to_audio>/audio.wav \
    -m_duration <path_to_model>/forward_tacotron_duration_prediction_att.xml \
    -m_forward <path_to_model>/forward_tacotron_regression_att.xml \
    -m_melgan <path_to_model>/melganupsample.xml
```
To run the demo, you can use public pre-trained models. You can download the pre-trained models with the OpenVINO
[Model Downloader](../../../tools/downloader/README.md).

> **NOTE**: Before running the demo with a trained model, make sure the model is converted to the Inference Engine
format (\*.xml + \*.bin) using the
[Model Optimizer tool](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html).

## Demo Output

The application outputs is WAV file with generated audio.

## See Also

* [Using Open Model Zoo Demos](../../README.md)
* [Model Optimizer](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html)
* [Model Downloader](../../../tools/downloader/README.md)
