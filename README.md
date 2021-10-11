# ROUGE for Multilingual Summarization

Since the original summarization metric [ROUGE](https://aclanthology.org/W04-1013/) is made only for English, we follow the method of [Hu et al.](https://aclanthology.org/D15-1229.pdf) and map words in other languages to numbers.

Languages without spaces (eg. Chinese, Japanese) will be segmented by characters and others will be split by spaces. For example, the Chinese text is split by characters, and the English words and numbers will be split by space.

```
[Input] Surface Phone将装载Windows 10 (The Surface Phone will be loaded with Windows 10)
[Segmentation] surface/phone/将/装/载/windows/10
```

## Install

``` shell
# install dependencies
pip install -r requirements.txt

# export environment paths
export PYROUGE_HOME_DIR=$(pwd)/ROUGE-1.5.5
export PYROUGE_TEMP_PATH=.

# add permission
chmod +x $PYROUGE_HOME_DIR/ROUGE-1.5.5.pl
```

## Usage
Each line in candidate/reference file should be a summary in the language ('-l') that consisting of sentences split by the delimiter (-d). '-t' indicates whether the text needs to be tokenized.

```
python3 calRouge.py -c example/candidate.txt -r example/reference.txt -l zh -d "<q>" -t
```

## ROUGE
If you have problem in using ROUGE, you can check the complete installation commands.

``` shell
sudo apt-get install libxml-perl libxml-dom-perl
pip install git+git://github.com/bheinzerling/pyrouge
export PYROUGE_HOME_DIR=the/path/to/RELEASE-1.5.5
pyrouge_set_rouge_path $PYROUGE_HOME_DIR
chmod +x $PYROUGE_HOME_DIR/ROUGE-1.5.5.pl
```

We have put the RELEASE-1.5.5 in the directory 'ROUGE-1.5.5'. You can also download [here](https://github.com/andersjo/pyrouge/tree/master/tools/ROUGE-1.5.5) by yourself. Remember to build Wordnet 2.0 instead of 1.6 in RELEASE-1.5.5/data:

```shell
# remove old files
rm $PYROUGE_HOME_DIR/data/WordNet-2.0-Exceptions/WordNet-2.0.exc.db
rm $PYROUGE_HOME_DIR/data/WordNet-2.0.exc.db

# create new files by yourself
cd $PYROUGE_HOME_DIR/data/WordNet-2.0-Exceptions/
perl ./buildExeptionDB.pl . exc WordNet-2.0.exc.db
cd ../
ln -s WordNet-2.0-Exceptions/WordNet-2.0.exc.db WordNet-2.0.exc.db
```
