# ChemHTS
ChemHTS (Chemical Hierarchical Tool Stacking) is a novel method designed to enhance the performance of Large Language Models (LLMs) in chemistry tasks by optimizing tool invocation pathways through a hierarchical stacking strategy

Our paper: [arXiv](https://arxiv.org/abs/2502.14327)

## Overview


![intro](png/intro.png)


## Start

### Install packages

```bash
conda create -n ChemHTS python=3.10
conda activate ChemHTS
pip install -r requirements.txt
```

### Add API keys in `template.env` and change its name to `.env`. 

```python
# AZURE for OpenAI Model
AZURE_API_KEY="your_api_key_here"
AZURE_API_ENDPOINT="your_api_endpoint_here"
AZURE_API_VERSION="your_api_version_here"
# ALI for Llama3 and Deepseek-R1
ALI_API_KEY="your_api_key_here"
```

If you use other API type, Please change the code in the `Stacking_agent/Basemodel.py`

### Tools

If you want to add new tools for your experiments, just create a new `.py` in the folder `Stacking_agent/tools`. And register your tool in `Stacking_agent/generator.py` with the following code:

```
self.tool_mapping = {
    ...
    'YourNewTool':'YourNewTool("param")'
    ...
}
```

### Run ChemHTS by running the following scripts

```bash
python main.py  --Task "ReactionPrediction" --tools "[SMILES2Property(),Chemformer()]"  --topN 5 --tool_number 2 --train_data_number 20
```

Or you can choose whatever stacking structures you want by adding the `--no_train --Stacking "Structures"`. For example:

```bash
python main.py --Task "Molecule_Design" --no_train --Stacking "['ChemDFM_1','Name2SMILES_0']" --topN 5 --tool_number 2 --train_data_number 10
```

### Ablation experiments
Run the Ablation experiment on parameters by running the following scripts
```bash
python ablation.py  --Task "Task" --tools "tools"  --topN topN --tool_number tool_number
```
And run the Multi-agent experiment with following scripts
```bash
python Multiagent.py --mode Chain --agents 0 --no_tool True
```

## Acknowledgement

The code of `Multiagent.py`  refers to [GPTSwarm](https://github.com/metauto-ai/GPTSwarm) and [AgentPrune](https://github.com/yanweiyue/AgentPrune.git)

## Citation

```bash
@misc{li2025chemhtshierarchicaltoolstacking,
      title={ChemHTS: Hierarchical Tool Stacking for Enhancing Chemical Agents}, 
      author={Zhucong Li and Jin Xiao and Bowei Zhang and Zhijian Zhou and Qianyu He and Fenglei Cao and Jiaqing Liang and Yuan Qi},
      year={2025},
      eprint={2502.14327},
      archivePrefix={arXiv},
      primaryClass={cs.CE},
      url={https://arxiv.org/abs/2502.14327}, 
}
```
