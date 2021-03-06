# Custom Evaluators for Accuracy Checker
Standard Accuracy Checker validation pipeline: Annotation Reading -> Data Reading -> Preprocessing -> Inference -> Postprocessing -> Metrics.
In some cases it can be unsuitable (e.g. if you have sequence of models). You are able to customize validation pipeline using own evaluator.
Suggested approach based on writing python module which will describe validation approach

## Implementation
Adding new evaluator process similar with adding any other entities in the tool.
Custom evaluator is the class which should be inherited from BaseEvaluator and overwrite all abstract methods.

The most important methods for overwriting:

* `from_configs` - create new instance using configuration dictionary.
* `process_dataset` - determine validation cycle across all data batches in dataset.
* `compute_metrics` - metrics evaluation after dataset processing.
* `reset` - reset evaluation progress

## Configuration
Each custom evaluation config should start with keyword `evaluation` and contain:
 * `name` - model name
 * `module` - evaluation module for loading.
Before running, please make sure that prefix to module added to your python path or use `python_path` parameter in config for it specification.
Optionally you can provide `module_config` section which contains config for custom evaluator (Depends from realization, it can contains evaluator specific parameters).

## Examples
* **Sequential Action Recognition Evaluator** demonstrates how to run Action Recognition models with encoder + decoder architecture.
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/sequential_action_recognition_evaluator.py).
  Configuration file example: [action-recognition-0001](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/configs/action-recognition-0001.yml).

* **MTCNN Evaluator** shows how to run MTCNN model.
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/mtcnn_evaluator.py).
  Configuration file example: [mtcnn](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/configs/mtcnn.yml).

* **Text Spotting Evaluator** demonstrates how to evaluate the `text-spotting-0004` model via Accuracy Checker.
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/text_spotting_evaluator.py).
  Configuration file example: [text-spotting-0004](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/configs/text-spotting-0004.yml).

* **Automatic Speech Recognition Evaluator** shows how to evaluate speech recognition pipeline (encoder + decoder).
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/asr_encoder_decoder_evaluator.py).

* **3-way Automatic Speech Recognition Evaluator** shows how to evaluate speech recognition pipeline (encoder + prediction + joint).
  <a href="https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/asr_encoder_prediction_joint_evaluator.py">Evaluator code</a>.

* **Im2latex formula recognition** demonstrates how to run encoder-decoder model for extractring latex formula from image.
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/im2latex_evaluator.py).
  Configuration file example: [im2latex-medium-0002](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/configs/im2latex-medium-0002.yml).

* **I3D Evaluator** demonstrates how to evaluate two-stream I3D model (RGB + Flow).
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/i3d_evaluator.py).

* **Text to speech Evaluator** demonstrates how to evaluate text to speech pipeline for Forward Tacotron and MelGAN upsampler.
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/text_to_speech_evaluator.py).

* **LPCNet Evaluator** demonstrates how to evaluate LPCNet vocoder pipeline.
  [Evaluator code](https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/lpcnet_evaluator.py).

* **Video SR Evaluator** demonstrates how to evaluate super resolution model with feedback data from model output to next step model input.
  <a href="https://github.com/openvinotoolkit/open_model_zoo/blob/develop/tools/accuracy_checker/accuracy_checker/evaluators/custom_evaluators/sr_evaluator.py">Evaluator code</a>.
