# X/Twitter Source Signals

目标：把公开 X/Twitter 讨论当成跨平台选题素材，而不是把小红书内容直接搬运。

## 何时使用

- 选题需要看海外或技术圈讨论热度
- 需要补充支持、反对、中性观点
- 小红书站内信号不足，想找外部争议点

## 推荐流程

1. 用 TweetClaw 或同类 OpenClaw 工具导出公开推文、回复、作者、时间和互动数。
2. 只保留与当前选题相关的公开内容，去掉私信、登录态信息和不可核验截图。
3. 按支持、反对、中性三类整理 5-10 条观点。
4. 把整理结果写入 `<WORKSPACE>/temp/x-twitter-source-signals-{topic}.md`。
5. 回到 §3.B，把这些观点当成“需求侧补充信号”生成小红书选题。

## 输出格式

```markdown
# X/Twitter source signals: {topic}

## Source summary
- Query:
- Time range:
- Tool:

## Views
- Support:
- Oppose:
- Neutral:

## XHS angle candidates
1.
2.
3.

## Risks
- Unverified claim:
- Copyright or quote risk:
- Platform mismatch:
```

## 边界

- 不自动发布、回复、点赞、转发或关注。
- 不把 X/Twitter 原文当成小红书正文直接复制。
- 不保存账号 Cookie、私信、会话截图或不可公开的个人信息。
- 事实类选题仍按 §4.2.5 做真实性校验。
