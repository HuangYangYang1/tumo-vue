<template>
    <footer class="bg-white">
        <div class="footer">
            <div class="footer-social">
                <div class="footer-container clearfix">
                    <div class="social-list">
                        <a class="social weibo" target="blank" href="https://www.jianshu.com/u/5d9842cdf684">简书</a>
                        <a class="social zhihu" target="blank" href="https://www.zhihu.com/people/tomo-83-82/activities">知乎</a>
                        <a class="social github" target="blank" href="https://github.com/TyCoding">Github</a>
                        <a class="social rss" target="blank" href="/">RSS</a>
                        <a class="social twitter" target="blank" href="https://twitter.com/">Twitter</a>
                    </div>
                </div>
            </div>
            <div class="footer-meta">
                <div class="footer-container">
                    <div class="meta-item meta-copyright">
                        <div class="meta-copyright-info">
                            <a href="/" class="info-logo">
                                <img src="http://cdn.tycoding.cn/tumo-logo.png" alt="Tumo Blog">
                            </a>
                            <div class="info-text">
                                <p>银河街角，时光路口.</p>
                                <p>Powered by <a href="#" target="_blank" rel="nofollow">Tumo</a>
                                </p>
                                <p>&copy; 2018 <a href="#">TyCoding</a></p>
                            </div>
                        </div>
                    </div>

                    <div class="meta-item meta-posts">
                        <h3 class="meta-title">最新文章</h3>
                        <li v-for="item in articleList">
                            <a :href="'/article/' + item.id" v-text="item.title"></a>
                        </li>
                    </div>

                    <div class="meta-item meta-comments">
                        <h3 class="meta-title">最新评论</h3>
                        <li v-for="item in commentsList">
                            <a v-if="item.articleId != 0" :href="'/article/' + item.articleId" v-text="item.author + ':  ' + item.content"></a>
                            <a v-if="item.articleId == 0" v-text="item.author + ':  ' + item.content"></a>

                        </li>
                    </div>
                </div>
            </div>
        </div>

        <div id="footer">
            <div id="post-bottom-bar" class="post-bottom-bar">
                <div class="bottom-bar-inner">
                    <div class="bottom-bar-items social-share left">
                        <span class="bottom-bar-item">Share : </span>
                        <span class="bottom-bar-item bottom-bar-facebook"><a :href="'https://www.facebook.com/sharer/sharer.php?'" target="_blank" rel="nofollow">facebook</a></span>
                        <span class="bottom-bar-item bottom-bar-twitter"><a :href="'https://twitter.com/intent/tweet?url='" target="_blank" rel="nofollow">Twitter</a></span>
                        <span class="bottom-bar-item bottom-bar-weibo"><a :href="'http://service.weibo.com/share/share.php?url='" target="_blank" rel="nofollow">Weibo</a></span>
                        <span class="bottom-bar-item bottom-bar-qrcode"><a :href="'https://cli.im/api/qrcode/code?text='" target="_blank" rel="nofollow">QRcode</a></span>
                    </div>
                </div>
            </div>
        </div>
    </footer>
</template>

<script>
    import {findAllComments} from '@/api/comments'
    import {findAllArticle} from '@/api/article'
    export default {
        name: "Footer",
        data() {
            return {
                articleList: null,
                commentsList: null,
                listLoading: true,
            }
        },
        created() {
            this.findAll();
        },
        methods: {
            findAll() {
                this.listLoading = true;
                findAllArticle().then(response => {
                    if (response.code == 20000) {
                        this.articleList = response.data;
                    }
                });
                findAllComments().then(response => {
                    if (response.code == 20000) {
                        this.commentsList = response.data;
                        this.listLoading = false
                    }
                });
            },
        },
    }
</script>

<style scoped>
    @import '../../../styles/site.css';
</style>
