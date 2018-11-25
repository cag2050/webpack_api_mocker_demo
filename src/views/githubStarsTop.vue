<template>
    <div>
        <table>
            <thead>
                <td>排名</td>
                <td>仓库名</td>
                <td style="width:100px;">star数</td>
                <td>仓库全名</td>
                <td>仓库地址</td>
            </thead>
            <tr v-for="(item, index) in items" :key="index">
                <td>{{index + 1}}</td>
                <td style="text-align: left;">{{item.name}}</td>
                <td>{{item.stargazers_count.toLocaleString()}}</td>
                <td style="text-align: left;">{{item.full_name}}</td>
                <td style="text-align: left;"><a :href="item.html_url" target="_blank">{{item.html_url}}</a></td>
            </tr>
        </table>
        <div v-show="loading">加载中...</div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'githubStarsTop',
    data () {
        return {
            items: [],
            loading: true
        }
    },
    created () {
        this.fetchList()
    },
    methods: {
        fetchList () {
            // axios.get('https://api.github.com/search/repositories?q=language:javascript&sort=stars')
            axios.get('/search/repositories?q=language:javascript&sort=stars')
                .then(res => {
                    this.items = res.data.items
                })
                .catch(err => {
                    throw err
                })
                .finally(() => {
                    this.loading = false
                })
        }
    }
}
</script>

<style scoped>

</style>
