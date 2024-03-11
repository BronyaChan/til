# Getting Pinboard article list via jq and convert to markdown format

The main purpose is to make it convenient when writing a weekly journal, so that you can copy and paste directly.

## Cutting corners version

```bash
export PINBOARD_TOKEN=your-api-token
curl -sS "https://api.pinboard.in/v1/posts/all?format=json&auth_token=$PINBOARD_TOKEN" \
    | jq -r '.[] | "- [\(.description)](\(.href)) - \(.extended)"'
```

The effect is to generate a markdown list in the following format

```md
- [simonw/til: Today I Learned](https://github.com/simonw/til/blob/main/ab/apache-bench-length-errors.md) - Consider using this format for TIL, only markdown will do, large chunks of code and images should be linked from outside. The key is to think deeply for each idea and be honest with yourself. Then reach a certain level of
- [Downloading a video should be “fair use” as recording a song from the radio | Hacker News --- Downloading videos should be considered "fair use" as recording a song from the radio | Hacker News](https://news.ycombinator.com/item?id=37112615) - Actually, I still don't understand whether this kind of downloading is illegal or not
- [A university teacher decides to deliver takeaways](https://mp.weixin.qq.com/s/cSL-Inf0QDKOPJd4yzkAGw) - \u003cblockquote\u003eAfter years spent working in an ivory tower, he wanted to break free from the confines, self-importance and sense of superiority.\u003c/blockquote\u003e
- [How China's Great Firewall Detects and Blocks Fully Encrypted Traffic](https://gfw.report/publications/usenixsecurity23/zh/) -
- [You’re probably using the wrong dictionary « the jsomers.net blog --- You're probably using the wrong dictionary « the jsomers.net blog](https://jsomers.net/blog/dictionary) - It turns out that a good dictionary can be so useful
- [Aggregate information intake and output using automated workflows | Reorx's Forge](https://reorx.com/blog/sharing-my-footprints-automation/) - \u003cblockquote\u003eShow how I used n8n to sync dynamic content from services like Twitter, YouTube, GitHub, and Douban to my personal Telegram Channel, achieving information aggregation for my personal digital life.\u003c/blockquote\u003e
- [nodebestpractices/README.chinese.md at master · goldbergyoni/nodebestpractices](https://github.com/goldbergyoni/nodebestpractices/blob/master/README.chinese.md) -
- [37% Law - MBA Think Tank Encyclopedia](https://wiki.mbalib.com/zh-tw/37%25%E6%B3%95%E5%88%99#:~:text=%5B%E7%B7%A8%E8%BC%AF%5D-,%E4%BB%80%E9%BA%BC%E6%98%AF37%25%E6%B3%95%E5%89%87,%E4%B9%9F%E5%B0%B1%E6%98%AF11%E5%80%8B%E6%88%BF%E5%AD%90%E3%80%82) - \u003cblockquote\u003e37% Rule, 37% Rule 37% Rule, comes from the book "The Algorithm of Beauty". It means that after mathematician Euler's experiment, 37% is used as the dividing point, and the time before it is used for observation, and the time after it is used for decision-making. For example, if you want to buy a house, there are 30 houses in the whole area, then you need to look at 37% of the houses first, which is 11 houses. Only look at the houses before 37% and don't buy them, but remember what you think is the best. After finishing, only start buying when encountering a house that is better than the best before.\u003c/blockquote\u003e
- [(Translation) Unicode Basics for Every Software Developer in 2023 | Gateway to the New World](https://blog.xinshijiededa.men/unicode/) - \u003cblockquote\u003eSince then, Python has progressed and CD-ROMs have become obsolete, but the rest still remain in UTF-16 or even UCS-2. Therefore, UTF-16 exists as an in-memory representation.
```

PS. Note that you need a proxy to access pinboard.in in mainland China

\u003e Fishy idea: shouldn't a better design be ny pinboard export --md ? The proxy and token are all set automatically. Pseudo-pinboard cli.

## References

- [pinboard password](https://pinboard.in/settings/password) - Token can be found here
- [pinboard api](https://pinboard.in/api) - You can also add more filter conditions, such as tag and time
- [jq Manual (development version)](https://stedolan.github.io/jq/manual/) - This can actually be asked to gpt, 'use jq command to parse, format as [description](href) - extended'
