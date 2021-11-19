- 👋 Hi, I’m @szzhangtao88
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
szzhangtao88/szzhangtao88 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
跳到内容
搜索或跳转到…
拉请求小号
问题
市场
探索
 
@szzhangtao88 
QIN2DIM
/
V2RayCloudSpider
民众
33
699173
代码
问题
1
拉取请求
讨论
行动
项目
1
维基
安全
洞察力
V2RayCloudSpider/.github/工作流程/ v2rss-probe.yaml
@QIN2DIM
QIN2DIM v5.6.6.beta.3
…
最新提交 4a599f9 on 8 Oct
 历史
 1 位 贡献者
75 行 (71 sloc)  3.47 KB
   
# 1. 此工作流使用预写指令为灵活的 Ubuntu 开发环境安装最新版 Google Chrome 以及对应版本的 ChromeDriver
# 2. 此工作流使用 env 环境变量定位 build.py 安装脚本以及 main.py 脚手架，若您的工程路径与默认配置不符请适当修改
名称: V2RSS 探针

＃   安排定时任务触发器默认值- cron的：'25 * * * *”表示为每25分钟执行一次
#   一般情况下建议不使用GitHub Actions部署v2rss-server，只有在你少用VPS 时在此构建服务
上：
  推：
    分支：[主]
  #时间表：
  #    - cron: '25 * * * *'

工作：
  构建：
    # ============================================
    # TODO [√] 指定工作流程
    # ============================================
    #必须选择ubuntu-latest以最高效率执行工作流，
    运行：ubuntu-latest

    # ============================================
    # TODO [√] 指定工作流程脚手架路径及必要启动参数
    # ============================================
    环境：
      #环境初始化脚本的相对路径如V2RaycSpider1225/build.py
      BUILDER：V2RaycSpider1225 / build.py
      #脚手架接口文件的相对路径如V2RaycSpider1225/main.py
      脚手架：V2RaycSpider1225/main.py
      # V2RSS 项目依赖文件的相对路径如V2RaycSpider1225/requirements.txt
      要求：V2RaycSpider1225/requirements.txt
      # UAtheK1nG 读取Secret Key 覆盖RedisMaster 配置
      UAtheK1nG : ${{ secrets.UAtheK1nG }}
    # ============================================
    # TODO [√] 检查工作分支及工作流程运行环境
    # ============================================
    步骤：
    -用途：动作/结帐@v2

    # ============================================
    # TODO [√]创建Python3.6+编译环境
    # ============================================
    -名称：设置 Python 3.8
      用途：动作/设置-python@v2
      与：
        蟒蛇版本：3.8
    # ============================================
    # TODO [√] 安装 Project 支持
    # ============================================
    #拉取要求
    -名称：安装依赖项
      运行：|
          python -m pip install --upgrade pip
          如果 [ -f ${{ env.REQUIREMENTS }} ]; 然后 pip install -r ${{ env.REQUIREMENTS }}; 菲
    # 1. 拉取最新版 Chrome 并适配对应版本的 ChromeDriver
    # 2. 初始化工作目录
    -名称：V2RSS 设置
      运行：|
        如果 [ -e ${{ env.BUILDER }} ]; 然后 python ${{ env.BUILDER }}; 菲
        如果 [ -e ${{ env.SCAFFOLD }} ]; 然后 python ${{ env.SCAFFOLD }} 构建；菲
    # ============================================
    # TODO [√] 测试脚手架脚手架经验
    # ============================================
    #执行一次数据库连接作业，检查正确的相关配置信息是否填写
    -名称：V2RSS ping
      运行：|
        如果 [ -e ${{ env.SCAFFOLD }} ]; 然后 python ${{ env.SCAFFOLD }} ping; 菲
    #执行一次清洗作业，检查订阅监听模块是否正常工作
    -名称：V2RSS 过期/解耦
      运行：|
        如果 [ -e ${{ env.SCAFFOLD }} ]; 然后 python ${{ env.SCAFFOLD }} 逾期；菲
        如果 [ -e ${{ env.SCAFFOLD }} ]; 然后 python ${{ env.SCAFFOLD }} --env=production decouple; 菲
    #执行一次采集作业，检查采集模块是否正常工作；使用 Spawn 习惯可不受限制地采集订阅
    -名称：V2RSS 生成
      运行：|
        如果 [ -e ${{ env.SCAFFOLD }} ]; 然后 python ${{ env.SCAFFOLD }} 生成；菲
© 2021 GitHub, Inc.
条款
隐私
安全
地位
文档
联系 GitHub
价钱
应用程序接口
训练
博客
关于
加载完成
