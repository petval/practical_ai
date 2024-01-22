# Práce na lokálním počítači
Většina kódu a modulů by měla být nezávislá na platformě, nicméně otestoval jsem pouze variantu Windows a Linux - MacOS by měl být pro naprostou většinu potřeb kurz v pohodě, ale ARM64 CPU podpora může teoreticky někde chybět (ale pro základní komponenty to nepředpokládám).

Co budete potřebovat:
- Python: [https://www.python.org/downloads/](https://www.python.org/downloads/)
- Conda pro vytváření Python prostředí: [https://docs.conda.io/projects/miniconda/en/latest/index.html](https://docs.conda.io/projects/miniconda/en/latest/index.html)
		Python ve verzi podporované Conda (leden 2024: 3.11)
- Visual Studio Code: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- Extension pro VSCode: ms-toolsai.jupyter a ms-python.python
- GitHub CLI nebo extension do VS Code (kvůli ověřování): [https://cli.github.com/](https://cli.github.com/)

Pak si stáhněte obsah kurzu z GitHub (přes git clone nebo jako zip).

Použijte Anaconda PowerShell Prompt ve Windows (najdete ve Start menu) nebo conda příkazy v běžném shellu v Linux či Mac a vytvořte conda prostředí ze souboru conda.yaml a v něm iPython kernel.

Vytvoříme teď virtuální prostředí s potřebnými balíčky. Níže jsou dvě varianty - první využívající Conda prostředí a Conda balíčky specifických verzí a druhá s Conda prostředí a balíčky pip bez omezení verze. Pokud by vám nějaké notebooky nefungovaly, můžete zkusit skočit do druhého prostředí.

```bash
# Go to cloned directory
cd practical_AI

# Option 1: Conda env with specific versions and Conda package manager
conda env create --name practical_AI -f conda.yaml
conda activate practical_AI
python -m ipykernel install --user --name practical_AI --display-name "Practical AI"

# Start VS Code from within so it finds the new environment and kernel
code

# Option 2: Conda env with pip package manager
conda create -n practical_AI_pip python=3.11
conda activate practical_AI_pip
pip install -r requirements.txt
python -m ipykernel install --user --name practical_AI_pip --display-name "Practical AI pip"

# Option CUDA GPU - valid for both options above
conda install --file requirements-cuda.txt  -c pytorch -c nvidia

# Start VS Code from within so it finds the new environment and kernel
code
```

Prostředí můžete kdykoli smazat a začít znovu, stačí z něj vyskočit (conda deactivate) a smazat (conda env remove -n practical_AI).

Pokud budte používat GPU, musíte mít příslušné CUDA drivery od NVIDIA a NVIDIA kartu (AMD je v Pytorch podporováno zatím jen v Linux, navíc některé open source modely AMD ani v takovém případě neumí využít). Řadu úloh lze dělat na CPU, zejména inferencing (využívání modelu), nicméně pro trénování a finetuning to může trvat opravdu dlouho. V takovém případě můžete zkrátit počet iterací (snížení množství epoch například) nebo zmenšit model. Pokud se chcete hodně zaměřit na ladění vlastních open source modelů, doporučuji raději pořídit VM v cloudu s rozumným GPU alespoň třídy NVIDIA T4 (a pokud se chcete rozmáchnout, tak A100 je ideální). T4 je z roku 2018 a v moderní generaci je jí blízko RTX 4060 (až na poloviční paměť, což je ale urovna u AI dost důležité).
