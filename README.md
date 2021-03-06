
[![Build Status](https://travis-ci.org/SSGL-SEP/t-sne_cruncher.png?branch=master)](https://travis-ci.org/SSGL-SEP/t-sne_cruncher) [![Code Climate](https://codeclimate.com/github/SSGL-SEP/t-sne_cruncher/badges/gpa.png)](https://codeclimate.com/github/SSGL-SEP/t-sne_cruncher) 

# Audio analyzer for [Speech explorer](https://github.com/SSGL-SEP/speech_explorer)

Typically reads data from .wav files and outputs json data used by [Speech explorer](https://github.com/SSGL-SEP/speech_explorer)

Feature extraction from wav files can currently be done with [mfcc](https://en.wikipedia.org/wiki/Mel-frequency_cepstrum), [fft](https://en.wikipedia.org/wiki/Fast_Fourier_transform), [mel-spectrogram](https://en.wikipedia.org/wiki/Mel_scale) or [chroma-stft](https://labrosa.ee.columbia.edu/matlab/chroma-ansyn/).

Dimensionality reduction can be performed in 3d or 2d with either [t-SNE](https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding) or [PCA](https://en.wikipedia.org/wiki/Principal_component_analysis).

Additionally `audio_concatenator.py` can be used to create a binary blob from the audio files used in the crunching process. The blob can be used by the [Speech explorer](https://github.com/SSGL-SEP/speech_explorer) to reduce the amount of network calls the application makes.

### [Environment](docs/environment.md)

### [crunch.py usage](docs/crunch_usage.md)

### [crunch.py technical documentation](docs/technical_documentation.md)

### [audio_concatenator.py usage](docs/audio_concatenator_usage.md)

### [Adding feature extraction algorithms](docs/feature_extraction.md)

![syllable map](docs/mfcc_syllable_30.png)
