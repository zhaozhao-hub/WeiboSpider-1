[中文说明](./README.md) | **English**

# WeiboSpider
<a href="https://github.com/nghuyong/WeiboSpider/stargazers">
    <img src="https://img.shields.io/github/stars/nghuyong/WeiboSpider.svg?colorA=orange&colorB=orange&logo=github"
         alt="GitHub stars">
  </a>
  <a href="https://github.com/nghuyong/WeiboSpider/issues">
        <img src="https://img.shields.io/github/issues/nghuyong/WeiboSpider.svg"
             alt="GitHub issues">
  </a>
  <a href="https://github.com/nghuyong/WeiboSpider/">
        <img src="https://img.shields.io/github/last-commit/nghuyong/WeiboSpider.svg">
  </a>
  <a href="https://github.com/nghuyong/WeiboSpider/blob/master/LICENSE">
        <img src="https://img.shields.io/github/license/nghuyong/WeiboSpider.svg"
             alt="GitHub license">
</a>

Continuously maintained Sina Weibo crawler 🚀🚀🚀

## Introduction

### Supported crawling types
- User Information
- Tweets post by user(all / specific period)
- Users' social relationships (fans/followers)
- Comments of tweets
- Tweets based on keywords and time period
- Retweets following a tweet

### Data Structure
The spider based on [weibo.cn](https://weibo.cn), and the crawled fields are very rich. More detail:[Data Structure Description](./.github/data_stracture.md)

## Get Started

### Pull the project && Install dependencies
Note that the Python Version is Python3.6
```bash
git clone git@github.com:nghuyong/WeiboSpider.git --depth 1 --no-single-branch
cd WeiboSpider
pip install -r requirements.txt
```
In addition, you need to install mongodb.

### Replace Cookies
Vist https://weibo.cn/

Log in, open the developer mode of the browser, and refresh again

![](./.github/images/cookie_from_chrome.png)

Copy the cookie value in the network in the weibo.cn data packet.

Edit `weibospider/settings.py`中:
```python
DEFAULT_REQUEST_HEADERS = {
    'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:61.0) Gecko/20100101 Firefox/61.0',
    'Cookie':'SCF=AlvwCT3ltiVc36wsKpuvTV8uWF4V1tZ17ms9t-bZCAuiVJKpCsgvvmSdylNE6_4GbqwA_MWvxNgoc0Ks-qbZStc.; OUTFOX_SEARCH_USER_ID_NCOO=1258151803.428431; SUB=_2A25zjTjHDeRhGeBN6VUX9SvEzT-IHXVQjliPrDV6PUJbkdANLUvskW1NRJ24IEPNKfRaplNknl957NryzKEwBmhJ; SUHB=0ftpSdul-YZaMk; _T_WM=76982927613'
}
```
Replace the cookie field with your own cookie

**If 403/302 appears on the crawler, it means that the account is blocked or the cookie is invalid**

## Add proxy IP (optional)
Rewrite the function [fetch_proxy](./weibospider/middlewares.py#6L), [more details](https://github.com/nghuyong/WeiboSpider/issues/124#issuecomment-654335439)

## Run the program

You can rewrite functions of `start_requests` in `./weibospider/spiders/*`

### Crawl User Info

```
cd weibospider
python run_spider.py user
```
![](./.github/images/user-spider.png)

### Crawl Fans List
```bash
python run_spider.py fan
```
![](./.github/images/fan-spider.png)


### Crawl Followers List
```bash
python run_spider.py follow
```
![](./.github/images/follow-spider.png)

### Crawl Comments of tweets
```bash
python run_spider.py comment
```
![](./.github/images/comment-spider.png)

### Crawl Tweets of Users(ALL)
`urls` select `init_url_by_user_id()` in the function of `start_requests` in `./weibospider/spiders/tweet.py`
```bash
python run_spider.py tweet
```
![](./.github/images/tweet-user-spider.png)

### Crawl Tweets of Users(Specific period)
`urls` select `init_url_by_user_id_and_date()` in the function of `start_requests` in `./weibospider/spiders/tweet.py`
```bash
python run_spider.py tweet
```
![](./.github/images/tweet-user-date.png)

### Crawl Retweet/Repost

```
python run_spider.py repost
```

![](./.github/images/repost-spider.png)