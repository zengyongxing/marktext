



# 结论

Github的private个人项目，用2000分钟/月的Github Actions就好。

如果需要内网On-Premise方式搭建自己的代码仓库，那么Jenkins吧。

# 对比表

|                      | Jenkins | TeamCity | Travis CI   | AppVeyor | Azure Pipeline       | circleci                   | Github  Action       | 阿里云效 |
| -------------------- | ------- | -------- | ----------- | -------- | -------------------- | -------------------------- | -------------------- | -------- |
| On-Premise           | yes     | yes      |             | yes      | yes                  |                            |                      |          |
| SaaS                 |         |          | Yes         | yes      | yes                  | yes                        | yes                  |          |
| Price for OpenSource | free    | free     | free        | free     | free                 | Free                       | free                 |          |
| Price for Private    | free    | free     | $69/月      | $29/月   | free for 1800分钟/月 | Free for Linux and Windows | free for 2000分钟/月 |          |
| Plugins              | 1600    | 366      |             |          | 970                  |                            |                      |          |
| SCM                  | Various | Various  | Github only | Various  | Various              |                            |                      |          |
| Trouble Shooting     | local   | local    | ?           | ssh      | ?                    |                            |                      |          |

