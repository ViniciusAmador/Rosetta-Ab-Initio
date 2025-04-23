[![Rosetta](https://img.shields.io/badge/ROSETTA-Protein%20Modeling-blue)](https://www.rosettacommons.org/)  
[![PSIPRED](https://img.shields.io/badge/PSIPRED-Secondary%20Structure%20Prediction-green)](http://bioinf.cs.ucl.ac.uk/psipred/)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Tutorial](https://img.shields.io/badge/Tutorial-Bioinformatics-green)
![Rosetta](https://img.shields.io/badge/Tool-Rosetta-blueviolet)
![Status](https://img.shields.io/badge/status-Active-brightgreen)
![Language](https://img.shields.io/badge/Written%20in-Markdown-orange)

<p align="center">
  <img src="assets/images1.png" width="300" alt="Rosetta">
</p>

# 🔬 Tutorial Rosetta: Geração de Fragmentos com PSIPRED e Modelagem Estrutural com AbinitioRelax | 🔬 Rosetta Tutorial: Fragment Generation with PSIPRED and Structure Modeling using AbinitioRelax | 🔬 Rosetta教程：使用PSIPRED生成片段并通过AbinitioRelax进行结构建模

## 🧬 Objetivo | Objective | 目标

Este tutorial descreve o processo de geração de fragmentos estruturais utilizando o PSIPRED e o fragment_picker do Rosetta, seguido da modelagem estrutural via AbinitioRelax.This tutorial describes the process of generating structural fragments using PSIPRED and Rosetta's fragment_picker, followed by structure modeling using AbinitioRelax.本教程介绍了使用 PSIPRED 和 Rosetta 的 fragment_picker 生成结构片段的过程，随后通过 AbinitioRelax 进行结构建模。

## 📁 Estrutura de Diretório | Directory Structure | 目录结构
```bash
/meu_projeto/  
│  
├── structure.fasta             # Sequência FASTA da proteína  
├── HevME1.psipred.ss2          # Resultado do PSIPRED (.ss2)  
├── flags_fragment              # Parâmetros do fragment_picker  
├── flags                       # Parâmetros do AbinitioRelax  
```
## 🔗 Etapa 1 – PSIPRED | Step 1 – PSIPRED | 第一步：PSIPRED

Acesse o site do PSIPRED:Go to the PSIPRED site:访问 PSIPRED 网站：👉 http://bioinf.cs.ucl.ac.uk/psipred/

Cole a sequência FASTA no campo.Paste the FASTA sequence in the field.将 FASTA 序列粘贴到输入框中。

Faça o download do arquivo PSIPRED raw scores in plain text format.Download the file PSIPRED raw scores in plain text format.下载文件 PSIPRED raw scores in plain text format。

Renomeie o arquivo para HevME1.psipred.ss2.Rename the file to HevME1.psipred.ss2.将文件重命名为 HevME1.psipred.ss2。

## 🧩 Etapa 2 – Fragment Picker | Step 2 – Fragment Picker | 第二步：片段选择器

🔸 2.1 Arquivos necessários | Required Files | 所需文件

Coloque os seguintes arquivos na mesma pasta:Place the following files in the same folder:将以下文件放入同一文件夹：
```bash
structure.fasta
HevME1.psipred.ss2
flags_fragment
```
🔸 2.2 Rodar fragment_picker | Run fragment_picker | 运行 fragment_picker

Execute primeiro para 3-mers e depois para 9-mers:First run for 3-mers, then for 9-mers:先运行 3-mers，再运行 9-mers：

# Exemplo Linux | Linux example | Linux 示例
```bash
./fragment_picker.linuxgccrelease @flags_fragment
```
# Exemplo macOS | macOS example | macOS 示例
```bash
./fragment_picker.macosclangrelease @flags_fragment
```
Exemplo de caminho completo no Linux:Full path example on Linux:Linux 中的完整路径示例：
```bash
[...]Rosetta/rosetta_bin_linux_2017.08.59291_bundle/main/source/bin/fragment_picker.linuxgccrelease @flags_fragment
```
Exemplo no macOS:Example on macOS:macOS 中的示例：
```bash
[...]/Rosetta/rosetta_bin_mac_2017.08.59291_bundle/main/source/bin/fragment_picker.macosclangrelease @flags_fragment
```
## 📄 Exemplo de flags_fragment comentado | Sample flags_fragment file with comments | 示例 flags_fragment 文件

### Nome do arquivo fasta | Fasta file | FASTA 文件
```bash
-fasta structure.fasta
```
### Nome da saída | Output name prefix | 输出名称前缀
```bash
-out:file:frag_prefix output_fragments
```
### Caminho para o arquivo PSIPRED | Path to PSIPRED file | PSIPRED 文件路径
```bash
-psipred_ss2 HevME1.psipred.ss2
```
### Tamanho dos fragmentos | Fragment sizes | 片段大小
```bash
-frags:frag_sizes 3 9
```
### Número de fragmentos | Number of fragments | 片段数
```bash
-frags:n_frags 200
```
### Utilizar base de dados de estruturas | Use vall database | 使用结构数据库
```bash
-frags:vall /caminho/para/vall.dat
```
## 🧱 Etapa 3 – AbinitioRelax | Step 3 – AbinitioRelax | 第三步：AbinitioRelax

Certifique-se de ter os arquivos:Make sure you have the following files:请确保你拥有以下文件：
```bash
structure.fasta
HevME1.psipred.ss2
fragments_3mers
fragments_9mers
flags
```
Execute o comando | Run the command | 运行命令：
```bash
[...]/Rosetta/rosetta_linux_bundle/main/source/bin/AbinitioRelax.static.linuxgccrelease @flags
```
⚠️ Dicas de Erros Comuns | Common Error Tips | 常见错误提示

✅ Arquivo .ss2 com nome errado: Verifique se está nomeado exatamente como referenciado no flags_fragment.

✅ Arquivo vall.dat ausente: O fragment_picker requer esse banco de dados para gerar os fragmentos. Baixe do site oficial do Rosetta.

✅ Incompatibilidade entre fasta e psipred: Certifique-se de que a sequência fasta corresponde exatamente à sequência usada no PSIPRED.

✅ Permissões de execução: Use chmod +x nos binários se estiverem sem permissão de execução.

📌 Referências | References | 参考文献

PSIPRED: http://bioinf.cs.ucl.ac.uk/psipred/
Rosetta Docs: https://www.rosettacommons.org/docs/latest/

Sali, A. & Blundell, T.L. (1993). Comparative Protein Modelling by Satisfaction of Spatial Restraints. J. Mol. Biol.

📬 Entre em contato para dúvidas ou sugestões!📬 Contact me for questions or suggestions!📬 如有问题或建议，请联系我！
