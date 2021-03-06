# fanfiction-nlp
NLP tools for fanfiction, based on David Bamman's BookNLP. Developed by CMU students beginning 2018.

# Running the pipeline
This script processes a directory of fanfiction files and extracts
 relevant text to characters, as well as fic AU metadata.
 
The script does:
* Character coreference
* Character feature extraction
	* Quote attribution
	* Assertion (facts about a character) attribution
* Character cooccurrence matrix
* Alternate universe (AU) extraction from fic metadata

## Requirements
* Python 2 and Python 3 (we're moving everything to Python 3 soon).

* Python packages: spaCy

* Parts of the pipeline use Stanford CoreNLP. You'll need to download [Stanford CoreNLP 3.9.2](https://stanfordnlp.github.io/CoreNLP/download.html). Unzip the downloaded file and find the file `stanford-corenlp-3.9.2-models.jar`. Place this file within the `CoreNLP` directory.

## Input 
Directory path to directory of fic chapter CSV files. 

If your input is raw text you'll need to format it like the examples in the `example_fandom` directory. [Here's](https://github.com/michaelmilleryoder/fanfiction-nlp/blob/master/example_fandom/10118594_0004.csv) an example. Eventually we'll support raw text file input.

## Output 
* Character coreference: 
	* a directory where fics are stored with cluster-level names appended after mentions, like this: "she ($\_hermione) and harry ($\_harry) walked through the woods".
	* a directory with files with cluster-level character names for each processed fic, one per line.

* Quote attribution: 
	* a directory with a JSON files for each fic. Each JSON file has cluster-level character names as keys and extracted and attributed quotes as keys.

* Assertion attribution: 
	* a directory where for each fic, there is a JSON file with keys as cluster-level character names and values with extracted assertions (statements or facts) about the character.

* Character cooccurrence matrix: 
	* description of output

* Alternative universe (AU) extraction:
	* a directory where for each fic, there is a list of predicted AU metadata tags, as well as confidence values in those predictions

## Command
`./run.sh`

<!---
`./run.sh <input_dir_path>`

`<collection_name>` of fics to be processed will be extracted from the directory name of the `<input_dir_path>`.

Output is automatically stored in `output/<collection_name>`.
--->

# Running the CoreNLP component for coreference clustering:

1. Git clone the repository.

2. Standford jars are present in the location mentioned in CoreNLP/jar-dir.

3. Copy the jars to the CoreNLP directory

4. Come back to the parent directory to run the RunCoreNLP.py file. The command runs the CoreNLP code over all the csv files    present in the folder specified and generate the formatted csv and txt files with coref resolution done.

5. Example Command: python RunCoreNLP.py example.fandom/ CharsOutputDir CorefOutputDir

   example.fandom/ : Directory containing all the csv files to be processed.
   
   CharsOutputDir  : Output Directory for all the characters files.
   
   CorefOutputDir  : Output Directory for all the coref resolution outputs (txt and csv ) files. 

6. CharOutputDir Directory contains the Character names (InputTextFileName.chars)

7. CorefOutputDir Directory contains the Coref resolution for the files (txt and csv format). ("InputTextFileName.coref.txt", InputTextFileName.coref.csv")

8. Example.fandom directory contains all the orginal csv files.

The search engine (WIP) has all the data under /usr2/scratch/fanfic indexed as of 10/30/2018 . Queries can be formed and run this way-
/path/to/search_engine/indri-5.0/runquery/IndriRunQuery -query="#uw2(Bilbo Baggins)" -count=5 -index=index


