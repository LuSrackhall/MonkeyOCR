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