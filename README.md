# LeCoder: A Large-Scale Automated Coder for Coding Errors in Word Production Tasks

This repository is for **LeCoder**, an automated error coding tool for word production tasks. It implements a data-driven approach, coding errors based on *cosine similarity in semantic vector representations* and *the normalized Levenshtein distance between IPA transcriptions* of target-response pairs. 

For more details on the methodology and evaluation, please refer to our paper (coming soon).

## I. Installation
Download the folder or clone the repository. It should contain the following files:
> + `LeCoder.exe`  
> + `LeCoder_Data.csv`
> + `README_GUI.md` (This File)  

`LeCoder.exe` is a standalone executable that does not require any additional software or dependencies to be installed.

To launch the tool, double-click on `LeCoder.exe`. A loading window will appear for approximately 30~60 seconds, after which the graphical user interface (GUI) will open.

## II. Input
To generate error codings, LeCoder requires input data in `.csv` or `.xlsx` format (if using `.xlsx`, the corresponding sheet name must be specified). You can load your data by clicking the `Browse` button to select the file, or by directly entering the file path.

The file must contain at least the following four columns: **Target**, **Response**, **TargetIPA**, and **ResponseIPA**. Column names are case- and whitespace-insensitive.

> **Target**: The stimulus.  
> **Response**: The participant's response. Can be an empty string if the response is a non-word.  
> **TargetIPA**: The simplified IPA transcription for the target word.  
> **ResponseIPA**: The simplified IPA transcription for the participant's response.

+ The **Response** column should contain only single-word responses (including compound words). If a participant produces a multiple-word response (e.g., "yellow fruit"), only one word (e.g., "fruit") should be recorded in the Response column.

## III. Parameters
In the parameter section, you can enter custom semantic and phonological thresholds. If these fields are left blank, LeCoder will use the default thresholds: semantic threshold = 0.298 and phonological threshold = 0.084. These values were trained and obtained using the standard 175-item Philadelphia Naming Test (PNT; Roach et al., 1996. See our paper for training details).

By clicking the `Suggest Parameters` button, LeCoder will automatically generate a suggested semantic threshold based on the average log<sub>10</sub> word frequency of the target words in your input data (SUBTLEXus; Brysbaert & New, 2009). Similarly, it will generate a suggested phonological threshold based on the average number of phonemes in target words.

The suggested values will appear in the corresponding input fields, displayed in grey. To apply these suggested values, please **manually type** them into the fields so the text appears **in black**. Otherwise, LeCoder will continue to use the default values.

> **Disclaimer**  
> Please note that the thresholds, especially the phonological threshold (*p*), is sensitive to average length and frequency. Therefore, if you have a small set of items, the suggestion may not be the optimum value. We recommend checking a small subset of data manually and adjusting the parameters accordingly.

Additionally, LeCoder provides an option to treat hypernym/hyponym responses as separate error codes (HR/HO) instead of categorizing them as semantic errors (S). 


## IV. Output
You can choose to overwrite the original file by checking the `Overwrite original file` box. Alternatively, you can enter a file name (with `.csv` or `.xlsx` extension), and LeCoder will create a new file with that name in the same folder as `LeCoder.exe`. You may also provide a full file path to save the output file to a specific location.

By clicking the `Run Error Coding` button, LeCoder will begin processing and generating the error coding. A progress bar will appear at the bottom of the GUI to indicate the process status.

The output will contain error codings for each input target-response pair, with the following coding scheme:
>**R**: Correct  
>**S**: Semantic error  
>**F**: Phonological error  
>**M**: Mixed error  
>**U**: Unrelated  
>**N**: Phonologically similar non-word  
>**NU**: Phonologically unrelated non-word  
>**NR**: No response  
>**HR**: Hypernym (if `hyperhyponym`=True, otherwise as **S**)  
>**HO**: Hyponym (if `hyperhyponym`=True, otherwise as **S**) 

## V. Data
We also include the data used to train LeCoder (See our paper for details on the datasets). To test LeCoder's perforamnce with this sample data, please first read the disclaimers below. Then remove the disclaimers from the `LeCoder_Data.csv` file so that LeCoder can load the data correctly.

Please note that the `LeCoder_Data.csv` file includes data from both datasets D1 and D2. The source dataset is specified in the **Subject ID** column. For example, subject D1P1 refers to the first participant from dataset D1.

> + **Disclaimer 1.**   
The human codes have taken into account dialectical and participant-specific variations in pronunciation, hence minor discrepancies between Response and ResponseIPA.
> + **Disclaimer 2.**  
We do not guarantee the accuracy of human coding. In fact, part of the claimed utility of LeCoder is that human coding could be inconsistent and/or error-prone.

## VI. References
+ For more details on LeCoder, please refer to our paper (coming soon).

+ Brysbaert, M., & New, B. (2009). Moving beyond Kučera and Francis: A critical evaluation of current word frequency norms and the introduction of a new and improved word frequency measure for American English. Behavior research methods, 41(4), 977-990.

+ Roach, A., Schwartz, M. F., Martin, N., Grewal, R. S., & Brecher, A. (1996). The Philadelphia naming test: scoring and rationale. Clinical aphasiology, 24, 121-134.
