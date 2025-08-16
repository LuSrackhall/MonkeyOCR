# Step 0. 安装Pixi包管理器

要安装 pixi，您可以在终端中运行以下命令:

* 可以使用 curl

  ```bash
  curl -fsSL https://pixi.sh/install.sh | sh
  ```

 或者

 可以使用 wget：

  ```bash
  wget -qO- https://pixi.sh/install.sh | sh
  ```

# Step 1. 安装MonkeyOCR和 PaddleX (CUDA支持、环境配置)
  
* 从github获取本仓库中使用Pixi管理依赖的monkeyOCR部署环境源码,并进入部署仓库目录:
  
  ```bash
  git clone https://github.com/LuSrackhall/MonkeyOCR.git
  ```
  
  ```bash
  cd MonkeyOCR
  ```

* 从github获取MonkeyOCR源码, 并进入MonkeyOCR源码目录:

  ```bash
  git clone https://github.com/Yuliang-Liu/MonkeyOCR.git
  ```

  ```bash
  cd MonkeyOCR
  ```

* 在MonkeyOCR源码目录内,使用以下命令从 GitHub 获取 PaddleX 最新源码：

  ```bash
  git clone https://github.com/PaddlePaddle/PaddleX.git
  ```
  
  或者

  如果访问 GitHub 网速较慢，可以从 Gitee 下载，命令如下：

  ```bash
  git clone https://gitee.com/paddlepaddle/PaddleX.git`
  ```

* 统一下载本步骤中所需的全部依赖:
  
  ```bash
  pixi i
  ```
  
# Step 2. 安装推理后端 (CUDA支持、环境配置)

MonkeyOCR项目官方推荐使用LMDeploy, 因此本部署仓库仅使用此方式进行部署。

仍是执行`pixi i`命令下载依赖, 直到执行结果为

> **✔ The default environment has been installed.**

代表环境配置成功。

<blockquote>
<details>
<summary>
[!IMPORTANT]

Fixing the **Shared Memory Error** on **20/30/40 series / V100 ...** GPUs (Optional)
......
</summary>

 Our 3B model runs smoothly on the NVIDIA RTX 30/40 series. However, when using **LMDeploy** as the inference backend, you might run into compatibility issues on these GPUs — typically this error:

 ```bash
 triton.runtime.errors.OutOfResources: out of resource: shared memory
 ```

 To resolve this issue, apply the following patch:

 ```bash
 python tools/lmdeploy_patcher.py patch
 ```

 **Note:** This command modifies LMDeploy’s source code in your environment.

 To undo the changes, simply run:

 ```bash
 python tools/lmdeploy_patcher.py restore
 ```

 Based on our tests on the **NVIDIA RTX 3090**, inference speed was **0.338 pages/second** using **LMDeploy** (with the patch applied), compared to only **0.015 pages/second** using **transformers**.

 **Special thanks to [@pineking](https://github.com/pineking) for the solution!**

</details>
</blockquote>

# Step 3. 下载模型权重

* 激活pixi环境

  ```bash
  pixi shell
  ```

* 下载模型权重 (注意, 在MonkeyOCR源码目录内执行以下命令)
  * 从 Huggingface 下载

    ```bash
    pip install huggingface_hub

    python tools/download_model.py -n MonkeyOCR  # or MonkeyOCR-pro-1.2B
    ```

  或者

  * 从 ModelScope 下载

    ```bash
    pip install modelscope

    python tools/download_model.py -t modelscope -n MonkeyOCR  # or MonkeyOCR-pro-1.2B
    ```

# 4. Inference、Gradio Demo、Fast API

到此为止, 以全部下载安装并配置完毕。

关于如何使用?

请直接参考[MonkeyOCR官方项目仓库](https://github.com/Yuliang-Liu/MonkeyOCR)的指南进行后续使用。
> 仅需确保激活Pixi虚拟环境, 且在MonkeyOCR源码目录下即可。