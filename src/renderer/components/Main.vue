<template>
    <div class="row" v-loading="loading">
        <div class="col-md-12">
            <ul class="article">
                <li v-for="item in items">
                    <div class="title">
                        <div class="favorite">
                            <strong><i class="el-icon-star-off"></i></strong>
                        </div>
                        <a :href="item.url" @click.prevent="navDetail(item)">{{item.title}}</a>
                        <div class="summary">{{item.summary}}</div>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    import cheerio from 'cheerio';
    import {shell} from 'electron'

    export default {
        name: "Main",
        data() {
            return {
                loading: true,
                items: []
            }
        },
        methods: {
            navDetail(item) {
                shell.openExternal(item.url)
            }
        },
        mounted() {
            this.$http.get('https://mac-torrent-download.net/').then(res => {
                const $ = cheerio.load(res.data);
                let $items = $('article.post');
                $items.each((i, o) => {
                    let $o = $(o);
                    this.items.push({
                        url: $o.find('a').prop('href'),
                        title: $o.find('a').text(),
                        summary: $o.find('div.smanone').text()
                    })
                });
                this.$nextTick(() => {
                    this.loading = false;
                })
            })
        }
    }
</script>

<style scoped>
    .article {
        list-style: none;
        padding-left: 0;
    }
    .article li {
        padding-bottom: 10px;
        border-bottom: 1px solid #eee;
        padding-top: 5px;
    }
    .article .favorite {
        position: absolute;
        font-weight: bold;
        cursor: pointer;
        left: 0;
        width: 28px;
        height: 26px;
        line-height: 26px;
    }
    .article .favorite:hover {
        color: #0056b3;
    }
    .title {
        font-size: 18px;
        padding-left: 28px;
        position: relative;
    }
    .title a {
    }
    .summary {
        font-size: 13px;
        color: #909399;
    }
</style>