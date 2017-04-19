# RobotReviewer

**Why the fork?** RobotReviewer3 is a big chunk of code that includes a web interface and a bunch of other stuff that isn't necessary for me. I'm interested in extracting PICO elements from medical citations (which is a small component of what RobotReviewer does).  

**How do you use it?** I have some code that uses this API for automatically extracting PICO elements, but it's private at the the moment. If you need to see it, please contact me.

_The original README is perserved below:_

Automatic extraction of data from clinical trial reports

RobotReviewer is a system for providing automatic annotations from clinical trials (in PDF format). Currently, RobotReviewer provides data on the trial *PICO* characteristics (Population, Interventions/Comparators, and Outcomes), and also automatically assesses trials for likely biases using the Cochrane Risk of Bias tool.

## Systematic review author?

This software is the *web-service* version, meaning it's aimed at people who make systematic review software.

**For most systematic review authors, if you want to try out RobotReviewer, you'd probably be better using the demo version on our website, available [here](https://robot-reviewer.vortext.systems).** If you like it, you could email the person who maintains your systematic review software a link to this site - they might be interested in adding it.

(Alternatively, individual authors who are adept at installing unix software from the terminal are free to install this version on their own machines by following the optional 'Web UI' instructions below).

## Developers of systematic review software?

RobotReviewer is open source and free to use under the GPL licence, version 3.0 (see the LICENCE.txt file in this repository).

We offer RobotReviewer free of charge, but we'd be most grateful if you would cite us if you use it. We're academics, and thrive on links and citations! Getting RobotReviewer widely used and cited helps us obtain the funding to maintain the project and make RobotReviewer better.

It also makes your methods transparent to your readers, and not least we'd love to see where RobotReviewer is used! :)

We'd appreciate it you could:

1. Display the text, 'Risk of Bias automation by RobotReviewer ([how to cite](http://vortext.systems/robotreviewer))' on the same screen or webpage on which the RobotReviewer results (highlighted text or risk of bias judgements) are displayed.
2. For web-based tools, the text 'how to cite' should link to our website `http://vortext.systems/robotreviewer`
3. For desktop software, you should usually link to the same website. If this is not possible, you may alternately display the text and example citations from the 'How to cite RobotReviewer' section below.

You can cite RobotReviewer as:

Marshall IJ, Kuiper J, & Wallace BC. RobotReviewer: evaluation of a system for automatically assessing bias in clinical trials. Journal of the American Medical Informatics Association 2015. [doi:10.1093/jamia/ocv044](http://dx.doi.org/10.1093/jamia/ocv044)

A BibTeX entry for LaTeX users is

    @article{RobotReviewer2015,
      title = {{RobotReviewer: evaluation of a system for automatically assessing bias in clinical trials}},
      author = {Marshall, Iain J and Kuiper, Jo\"{e}l and Wallace, Byron C},
      doi = {10.1093/jamia/ocv044},
      url = {http://dx.doi.org/10.1093/jamia/ocv044},
      journal = {Journal of the American Medical Informatics Association},
      year = {2015}
      month = jun,
      pages = {ocv044}
    }


## Installation

1. Ensure you have a working version of Python 2.7+ or 3.4+. We recommend using Python from the [Anaconda Python distribution](https://www.continuum.io/downloads) for a quicker and more reliable experience. However, if you have Python already installed that will probably work fine too.

2. Get a copy of the RobotReviewer repo, and go into that directory
    ```bash
    git clone https://github.com/ijmarshall/robotreviewer3.git
    cd robotreviewer3
    ```

3. Get the large data files (>1GB) via git lfs (`brew install git-lfs` if you don't have it)
    ```bash
    git lfs install
    git lfs pull
    ```

**NB** Step 3 seems to be a bit unreliable... If following those steps does not result in some large files being downloaded, please try updating your version of `git`, and `git lfs` which seems to solve the problem in most cases. If it doesn't please [contact us](mailto:mail@ijmarshall) and we'll try our best to help.

3. Install the Python libraries that RobotReviewer needs - do one of the following.

    a. If you are using Anaconda:

```bash
conda config --add channels spacy  # only needed once
conda install flask numpy scipy scikit-learn spacy
pip install fuzzywuzzy # (this is not yet in the anaconda repo)
```

    b. For everyone else:

```bash
pip install flask numpy scipy scikit-learn spacy fuzzywuzzy
```

4. Install the sentence processing data:
```bash
python -m spacy.en.download
```
      
5. This version of RobotReviewer requires Grobid, which in turn uses Java. Follow the instructions [here](https://grobid.readthedocs.io/en/latest/Install-Grobid/) to download and build it.

6. Edit the `robotreviewer/config.py` file to contain the path to the directory where you have installed Grobid. (RobotReviewer will start it automatically in a subprocess). Note that this should be the path to the entire (parent) Grobid directory, not the bin subfolder. 

## Running

The following

```bash
python -m robotreviewer
```

will start a flask server running on `http://localhost:5000`. You can run the server in development mode by passing `DEBUG=true python -m robotreviewer`. Visiting this address from a browser will show the new multiple PDF synthesis demonstration.

## Rest API

The big change in this version of RobotReviewer is that we now deal with *groups* of clinical trial reports, rather than one at a time. This is to allow RobotReviewer to synthesise the results of multiple trials.

As a consequence API has become more sophisticated than previously, and we will add further documentation about it here.

In the meantime, the code for the API endpoints can be found in `/robotreviewer/app.py`. 

Some things remain simple; e.g., for an example of using RR to classify abstracts as RCTs (or not) see [this gist](https://gist.github.com/bwallace/beebf6d7bbacfbb91704f66c28dcc537). 

If you are interested in incorporating RobotReviewer into your own software, please [contact us](mailto:mail@ijmarshall) and we'd be pleased to assist.


## Help

Feel free to contact us on [mail@ijmarshall.com](mailto:mail@ijmarshall) with any questions.

## References

1. Marshall, I. J., Kuiper, J., & Wallace, B. C. (2015). RobotReviewer: evaluation of a system for automatically assessing bias in clinical trials. Journal of the American Medical Informatics Association. [[doi]](http://dx.doi.org/10.1093/jamia/ocv044)
2. Zhang Y, Marshall I. J., & Wallace, B. C. (2016) Rationale-Augmented Convolutional Neural Networks for Text Classification. Conference on Empirical Methods on Natural Language Processing. [[preprint]](https://arxiv.org/pdf/1605.04469v2.pdf)
2. Marshall, I., Kuiper, J., & Wallace, B. (2015). Automating Risk of Bias Assessment for Clinical Trials. IEEE Journal of Biomedical and Health Informatics. [[doi]](http://dx.doi.org/10.1109/JBHI.2015.2431314)
3. Kuiper, J., Marshall, I. J., Wallace, B. C., & Swertz, M. A. (2014). Spá: A Web-Based Viewer for Text Mining in Evidence Based Medicine. In Proceedings of the European Conference on Machine Learning and Principles and Practice of Knowledge Discovery in Databases (ECML-PKDD 2014) (Vol. 8726, pp. 452–455). Springer Berlin Heidelberg. [[doi]](http://dx.doi.org/10.1007/978-3-662-44845-8_33)
4. Marshall, I. J., Kuiper, J., & Wallace, B. C. (2014). Automating Risk of Bias Assessment for Clinical Trials. In Proceedings of the ACM Conference on Bioinformatics, Computational Biology, and Health Informatics (ACM-BCB) (pp. 88–95). ACM. [[doi]](http://dx.doi.org/10.1145/2649387.2649406)

Copyright (c) 2016 Iain Marshall, Joël Kuiper, and Byron Wallace

## Support

This work is supported by: National Institutes of Health (NIH) under the National Library of Medicine, grant R01-LM012086-01A1, "Semi-Automating Data Extraction for Systematic Reviews", and by NIH grant 5UH2CA203711-02, "Crowdsourcing Mark-up of the Medical Literature to Support Evidence-Based Medicine and Develop Automated Annotation Capabilities", and the UK Medical Research Council (MRC), through its Skills Development Fellowship program, grant MR/N015185/1
