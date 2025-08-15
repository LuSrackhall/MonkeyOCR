# Step 1. Install PaddleX

* To install pixi you can run the following command in your terminal:
  * `curl -fsSL https://pixi.sh/install.sh | sh`

  Or, if your system doesn't have curl, you can use wget:

  * `wget -qO- https://pixi.sh/install.sh | sh`
  
* 从github获取本仓库中使用Pixi管理依赖的monkeyOCR部署环境源码,并进入部署仓库目录:
  
  * `git clone https://github.com/LuSrackhall/MonkeyOCR.git`
  
  * `cd MonkeyOCR`

* 从github获取MonkeyOCR源码, 并进入MonkeyOCR源码目录:

  * `git clone https://github.com/Yuliang-Liu/MonkeyOCR.git`

  * `cd MonkeyOCR`

* 在MonkeyOCR源码目录内,使用以下命令从 GitHub 获取 PaddleX 最新源码：
  * `git clone https://github.com/PaddlePaddle/PaddleX.git`

  如果访问 GitHub 网速较慢，可以从 Gitee 下载，命令如下：
  * `git clone https://gitee.com/paddlepaddle/PaddleX.git`

* 统一下载本步骤中所需的全部依赖:
  
  * `pixi i`
  
# Step 2. Install Inference Backend

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
 
 ```
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

