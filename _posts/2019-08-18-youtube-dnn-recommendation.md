---
layout: post
title: "Deep Neural Network for YouTube Recommendation 论文笔记"
date: 2019-08-18
excerpt: "youtube 基于dnn的推荐系统."
tag: 
- dnn
- recommendation
comments: true
---

这篇论文 Deep Neural Networks for YouTube Recommendations 是google的YouTube团队在推荐系统上DNN方面的尝试，发表在16年9月的RecSys会议。虽然国内必须翻墙才能登录YouTube，但想必大家都知道这个网站。基本上算是世界范围内视频领域的最大的网站了，坐拥10亿量级的用户，网站内的视频推荐自然是一个非常重要的功能。本文就focus在YouTube视频推荐的DNN算法，文中不但详细介绍了Youtube推荐算法和架构细节，还给了不少practical lessons and insights，很值得精读一番。下图便是YouTube APP视频推荐的一个例子。

在推荐系统领域，特别是YouTube的所在视频推荐领域，主要面临三个挑战：

规模大：用户和视频的数量都很大，只能适应小规模数据集的算法就不考虑了。
更新快：youtube视频更新频率很高，每秒有小时级别的视频上传，需要在新发布视频和已有存量视频间进行balance。更新快（实时性）的另一方面的体现是用户实时行为切换很快，模型需要很好的追踪用户的实时行为。
噪音：噪音主要体现在用户的历史行为往往是稀疏的并且是不完整的，并且没有一个明确的ground truth的满意度signal，我们面对的都是noisy implicit feedback signals。噪音另一个方面就是视频本身很多数据都是非结构化的。这两点对算法的鲁棒性提出了很高的挑战。
之所以要在推荐系统中应用DNN解决问题，一个重要原因是google内部在机器学习问题上的通用solution的趋势正转移到Deep learning，系统实际部署在基于tensorflow的Google
Brain上。
