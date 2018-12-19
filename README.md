
# VGS-dataset-metadata

## Japanese dataset and metadata
**The Japanese dataset we used for our experiments is now [avaiblable on Zenodo](https://doi.org/10.5281/zenodo.1495070) ([![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.1495070.svg)](https://doi.org/10.5281/zenodo.1495070))**
This dataset consists of synthetically spoken captions for the [STAIR dataset](https://arxiv.org/abs/1705.00823). Following the same methodology as Chrupała _et al._ (see [article](https://arxiv.org/abs/1702.01991) | [dataset](https://zenodo.org/record/400926#.W_er6mVKjmH) | [code](https://github.com/gchrupala/visually-grounded-speech)) we generated speech for each caption of the STAIR dataset using Google's Text-to-Speech API.

This dataset was used for visually grounded speech experiments (paper submitted at ICASSP2019, pending review).

The dataset comprises the following files :

-   **mp3-stair.tar.gz** :  MP3 files of each caption in the STAIR dataset. Filenames have the following pattern _imageID_captionID_, where both _imageID_ and _captionID_ correspond to those provided in the original dataset (see annotation format [here](http://captions.stair.center/download/))
-   **dataset.mfcc.npy** : Numpy array with MFCC vectors for each caption. MFCC were extracted using [python_speech_features](https://github.com/jameslyons/python_speech_features) with default configuration. To know to which caption the MFCC vectors belong to, you can use the files dataset.words.txt and dataset.ids.txt.
-   **dataset.words.txt** : Captions corresponding to each MFCC vector (line number = position in Numpy array, starting from 0)
-   **dataset.ids.txt** : IDs of the captions (_imageID_captionID_) corresponding to each MFCC vector (line number = position in Numpy array, starting from 0)
-   Splits (*splits* exactly correspond to those used by [Chrupała _et al._](https://arxiv.org/abs/1702.01991))
    -   test
        -   **test.txt** : captions comprising the test split
        -   **test_ids.txt**: IDs of the captions in the test split
        -   **test_tagged.txt** : tagged version of the test split
        -   **test-alignments.json.zip** : Forced alignments of all the captions in the test split. (dictionary where the key corresponds to the caption ID in the STAIR dataset). _Due to an unknown error during upload, the JSON file had to be zipped..._
    -   train
        -   **train.txt** : captions comprising the train split
        -   **train_ids.txt** : IDs of the captions in the train split
        -   **train_tagged.txt** : tagged version of the train split
    -   val
        -   **val.txt** : captions comprising the val split
        -   **val_ids.txt** : IDs of the captions in the val split
        -   **val_tagged.txt** : tagged version of the val split

## Synthetically spoken COCO metadata
Metadata of the synthetically spoken COCO dataset (by [Chrupała _et al._](https://arxiv.org/abs/1702.01991)) is to be found in this repository: **[synth-coco-metadata.json](https://github.com/William-N-Havard/VGS-dataset-metadata/blob/master/synth-coco-metadata.json "synth-coco-metadata.json")**

## Metadata format
**Metadata was structured as follows:**

Each JSON file contains a *dict* where the key corresponds to the caption ID in each dataset. The value associated with each *dict* is the following:

*English*
```python
{
 'audio_length': 5.0, #length of WAV file (in seconds)
 'forced_alignments': {
                       # alignments at phone level
                       'phones': [{'end': 0.03, 'label': 'sil', 'start': 0.0},
                                  ...
                                  {'end': 3.46, 'label': 'sp', 'start': 3.19}],
                                  
                       # alignments at word level
                       'words': [{'end': 0.18, 'label': 'a', 'start': 0.03},
								 ...
                                 {'end': 3.19, 'label': 'wall', 'start': 2.85}],
                                 
                       # POS tag of each word
                       'tags': [{'end': 0.18, 'label': 'DT', 'start': 0.03},
                                ...
                                {'end': 3.19, 'label': 'NN', 'start': 2.85}]}
}
```

*Japanese*
```python
{
 'audio_length': 3.744, #length of WAV file (in seconds)
 'forced_alignments': {
                       # alignments at phone level
                       'phones': [{'end': 0.18, 'label': 'i', 'start': 0.0},
                                  ...
                                  {'end': 3.46, 'label': 'u', 'start': 3.38}],
                       # alignments at word level (X-SAMPA)
                       'words': [{'end': 0.51, 'label': 'imai', 'start': 0.0},
                                 ...
                                 {'end': 3.46, 'label': 'ru', 'start': 3.31}],
                       
                       # Hiragana transcription of each word          
                       'hiragana': [{'end': 0.51, 'label': 'いまい', 'start': 0.0},
                                    ...
                                    {'end': 3.46, 'label': 'る', 'start': 3.31}],
                                    
                       # Original text (Kanji/Hiragana/Katakana/Romaji)
                       'kanji': [{'end': 0.51, 'label': '今井', 'start': 0.0},
                                 ...
                                 {'end': 3.46, 'label': 'る', 'start': 3.31}],
                                 
                       # POS tag of each word (Kytea)
                       'tags': [{'end': 0.51, 'label': 'N', 'start': 0.0},
                                ...
                                {'end': 3.46, 'label': 'TAIL', 'start': 3.31}]
}
```                        
