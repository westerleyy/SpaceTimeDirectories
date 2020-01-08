### NYU x NYPL Space Time Directories
This repository serves to consolidate all of the scripts required to operationalize the digitization process of New York City's 19th century directories.  

#### Current Status @westerleyy
As of January 7, 2020, a workflow for the preprocessing of the images has been developed. At this moment, it sits within the `WorkflowTrial01.ipynb` file. The present workflow will crop out images to just the columns and then perform an affine transformation which effectively deskews and rotates the image.  
The `crop_for_columns.py` file operationalizes for bash command line operations.  
  
#### Tesseract -oem and -psm values  
`-psm` stands for Page Segmentation Modes. This [page](https://github.com/tesseract-ocr/tesseract/wiki/ImproveQuality#page-segmentation-method) explains in detail how it works but basically there are 14 options as listed below:  

Page Segmentation Modes:  
  0    Orientation and script detection (OSD) only.  
  1    Automatic page segmentation with OSD.  
  2    Automatic page segmentation, but no OSD, or OCR.  
  3    Fully automatic page segmentation, but no OSD. **(Default)**  
  4    Assume a single column of text of variable sizes.  
  5    Assume a single uniform block of vertically aligned text.  
  6    Assume a single uniform block of text.  
  7    Treat the image as a single text line.  
  8    Treat the image as a single word.  
  9    Treat the image as a single word in a circle.  
 10    Treat the image as a single character.  
 11    Sparse text. Find as much text as possible in no particular order.  
 12    Sparse text with OSD.  
 13    Raw line. Treat the image as a single text line, bypassing hacks that are Tesseract-specific.    
   
Changing any of the Page Segmentation Nodes options will not signficantly improve the performance of the Tesseract. It appear that `-psm` = 5 is designed with Asian languages such as Chinese, Japanese, and Korean in mind.   
Most of the options describe text formats that are unlike those in the directories. OSD will not be helpful because deskewing and rotation will already have taken place and the language of the directory is English. There might be non-English last names such as Núnez for example, but they are not significantly different from English to warrant changing the `psm` modes.  
  
`-oem` stands for OCR Engine Mode. Tesseract's own [readme](https://github.com/tesseract-ocr/tesseract/wiki/ReadMe) is not particularly helpful. This [page](https://www.learnopencv.com/deep-learning-based-text-recognition-ocr-using-tesseract-and-opencv/) provides more information on the OEM options available. 

OCR Engine Modes:  
  0    Legacy engine only.  
  1    Neural nets LSTM engine only.  
  2    Legacy + LSTM engines. **(default)**  
  3    Default, based on what is available.  
    
Of these four options, the default `-oem` option appears to be the best. 

#### Current List of Hyperparameters

1. Pre-crop processing: Edge detection, dilation etc. 

2. Post-crop processing: Deskew and image rotation.

3. Tesseract `-oem` and `-psm` values: 2 and 3 respectively 

4. hocr-detect columns?

5. CRF extracted features and amount of training data 
