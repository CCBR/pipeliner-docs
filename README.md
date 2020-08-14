# Pipeliner Documentation  
Pipeline *Runner*, also known as Pipeline*r*, is an open-source and scalable solution for analyzing next-generation sequencing data. Pipeliner provides access to the same best-practices NGS pipelines developed and benchmarked by experts at [CCBR](https://ccbr.ccr.cancer.gov/) and [NCBR](https://ncbr.ncifcrf.gov/). This repository is the main source of documentation for users and developers working with or contributing to [Pipeline*r*](https://github.com/CCBR/Pipeliner).

### Installation
```bash
# Clone the Repository
git clone https://github.com/skchronicles/pipeliner-docs.git
# Create a virtual environment
python3 -m venv .venv
# Activate the virtual environment
. .venv/bin/activate
# Update pip
pip install --upgrade pip
# Download Dependencies
pip install -r requirements.txt
```

### Preview while editing  
MkDocs includes a previewing server, so you can view your update live and as you write your documentation. The server will automatically rebuild the site upon saving.  
```bash
# Activate the virtual environment
. .venv/bin/activate
# Start serving your documentation
mkdocs serve
```

### Build static site  
Once you are content with your changes, you can build the static site:  
```bash
mkdocs build
```
