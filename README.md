To run:

1. In Git Bash:
2. cd to project directory
3. had to `set JEKYLL_ENV=production` [described here](https://mademistakes.com/mastering-jekyll/site-url-baseurl/#jekyll-development-and-siteurl)
4. `bundle exec jekyll serve`
5. go to http://localhost:4000/recipe-box/ in browser

due to some [webrick nuance/bug](https://github.com/jekyll/jekyll/issues/6709) urls wont work locally without a trailing slash 
- http://localhost:4000/recipe-box wont work, but with a trailing slash will

For further information:
- [github pages url](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll)
- [jekyll url](https://jekyllrb.com/docs/installation/windows/)