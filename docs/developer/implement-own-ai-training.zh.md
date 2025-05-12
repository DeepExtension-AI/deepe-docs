
# 🛠️ 如何实现你自己的训练逻辑

DeepExtension 允许你将自定义的 AI 训练代码集成到其 UI 驱动的训练流程中。  
只要你的代码能在本地 Python 环境中正常运行，它就几乎可以被扩展到 DeepExtension 中使用。

本文将介绍如何通过 `custom01.py` （或 `custom02.py`） 将自定义训练脚本注册为可视化界面可用的方法。

---

## 🚀 基本思路

只要满足以下条件，你的训练代码就可以被 DeepExtension 接管运行：

- 能接受从 UI 传入的参数
- 支持日志回调（用于实时记录训练状态）
- 使用标准接口保存模型与 tokenizer

本质上，你只需要做：

1. 把你的训练代码粘贴到指定模板中  
2. 把 UI 参数连接到你的代码中  
3. 注册日志回调函数  
4. 留下模型保存与训练启动给 DeepExtension 自动执行

---

## 📁 涉及的文件

在 Docker 工作目录下，进入 `training/` 目录，你会看到以下文件：

- `custom-template.py`  
- `run_local_train_test_template.py`  
- `test-training-code.py`  

> ⚠️ 不要修改这些模板文件，它们是参考模板，仅供复制使用。

---

## 🧪 准备你的自定义训练脚本

假设你现在要实现 `custom01.py`，它在 **Training Method Management** 页面中注册。

### 步骤 1：复制模板文件

```bash
cp custom-template.py custom01.py
```

如果 `custom01.py` 已存在，请提前备份。

### 步骤 2：插入你的代码到指定位置

在 `custom01.py` 中，你会看到以下结构：

```python
#============ from here add your own train code

#============ end here with your own train code
```

把你完整的训练逻辑粘贴到这两个注释之间。

你先前的代码需要定义以下对象：

- `model`：具有 `save_pretrained()` 方法  
- `tokenizer`：具有 `save_pretrained()` 方法  
- `trainer`：具有 `train()` 方法  

如变量名不同，请改名为以上标准名称。

### 步骤 3：连接参数

将以下变量（由 UI 传入）正确地映射到你的训练代码中：

```text
MODEL_PATH, MAX_SEQ_LENGTH, LORA_RANK, LOAD_IN_4BIT
DATASET_PATH, MAX_INPUT_LENGTH, MAX_CONTENT_LENGTH, MAX_SAMPLES
NUM_GENERATIONS, MAX_GRAD_NORM, OUTPUT_DIR, MAX_STEPS
BATCH_SIZE, GRAD_ACCUM_STEPS, LEARNING_RATE, WARMUP_STEPS
PromptInputColumn, PromptOutputColumn
```

> 🚨 至少 `MODEL_PATH` 和 `DATASET_PATH` 是必须使用的。

### 步骤 4：绑定日志回调

在初始化 `trainer` 时，增加如下代码：

```python
trainer = ...(
    callbacks=[callback],
)
```

这是为了让 DeepExtension UI 能实时查看训练日志和指标。

### 步骤 5：删除训练与保存的手动调用

在你自己的代码中不要显式调用以下方法：

```python
trainer.train()
model.save_pretrained(...)
tokenizer.save_pretrained(...)
```

如果有请删除相关代码。这些会由 DeepExtension 自动完成。

---

## 🧪 本地测试自定义训练代码

在 UI 中正式运行前，建议你先在本地测试该方法。

### A. 复制测试模板

```bash
cp run_local_train_test_template.py run_local_train_test.py
```

### B. 修改以下字段

在 `run_local_train_test.py` 中修改：

- `'your-model_path'` → 一个注册过的 base model 的绝对路径
- `'your-dataset_path'` → 数据集的绝对路径
- `'your-output_dir'` → 保存临时训练结果的输出目录
- `'your-custom-file.py'` → 改为 `custom01.py`
- 其他参数可根据需要微调

### C. 执行测试

```bash
python run_local_train_test.py
```

### D. 验证结果

确认：

- 训练过程能顺利运行完毕  
- 输出文件正确写入 `your-output_dir`  

---

## ✅ 准备就绪

如果测试通过，你现在就可以通过 DeepExtension UI 使用 **Custom01_Train** 启动训练任务了。

有关训练任务的启动方法，请参考：  
📘 [模型训练模块](../user-guide/model-training.md)

---

*DeepExtension — 让你的自定义训练代码无缝集成到企业级 AI 流水线中。*
