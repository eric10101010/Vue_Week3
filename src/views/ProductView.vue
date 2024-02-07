<template>
    <div class="container mt-3">
        <div class="row py-3">
            <div class="col-md-10">
                <div class="d-flex justify-content-between">
                    <h2>產品列表</h2>
                    <button class="btn btn-primary text-white" @click="openModal('new')">建立新產品</button>
                </div>  
            <table class="table table-hover mt-4">
                <thead>
                    <tr>
                        <th width="150">產品名稱</th>
                        <th width="120">原價</th>
                        <th width="120">售價</th>
                        <th width="150">是否啟用</th>
                        <th width="160">編輯產品</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in productsList" :key="item.id">
                        <td width="150">{{ item.title }}</td>
                        <td width="120">{{ item.origin_price }}</td>
                        <td width="120">{{ item.price }}</td>
                        <td width="150">
                            <span v-if="item.is_enabled" class="text-success" >啟用</span>
                            <span v-else>未啟用</span>
                        </td>
                        <!-- <td width="120">
                            <button type="button" 
                                    class="btn btn-outline-primary" 
                                    @click="checkDetail(item)"
                            >
                            查看細節
                            </button>
                        </td> -->
                        <td width="160" class="d-flex justify-content-between">
                            <button type="button" class="btn btn-primary text-white" @click="openModal('edit', item)">
                            編輯
                            </button>
                            <button type="button" class="btn btn-danger" @click="openModal('delete', item)">
                            刪除
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
            <p>目前有 <span class="text-success">{{ productsList.length }}</span> 項產品</p>
            <ProductModal :tempProduct="tempProduct"></ProductModal>
            </div>
        </div>
    </div>
    <div id="productModal" ref="productModal" class="modal fade" tabindex="-1" aria-labelledby="productModalLabel"
            aria-hidden="true">
        <div class="modal-dialog modal-xl">
            <div class="modal-content border-0">
            <div class="modal-header bg-dark text-white">
                <h5 id="productModalLabel" class="modal-title">
                <span>新增產品</span>
                </h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <div class="row">
                <div class="col-sm-4">
                    <div class="mb-2">
                        <div class="mb-3" v-if="tempProduct.imagesUrl.length === 0">
                            <label for="imageUrl" class="form-label">輸入圖片網址</label>
                            <input type="text" class="form-control"
                                    placeholder="請輸入圖片連結" v-model="tempProduct.imageUrl">
                        </div>
                        <img class="img-fluid" :src="tempProduct.imageUrl">
                    </div>
                    <h3 class="mb-3">多圖新增</h3>
                    <div v-if="Array.isArray(tempProduct.imagesUrl)"> 
                        <div class="mb-1">
                            <div class="mb-1" v-for="(image, key) in tempProduct.imagesUrl" :key="key + 123">
                                <label class="form-label">圖片網址</label>
                                <input type="text" class="form-control" v-model="tempProduct.imagesUrl[key]"
                                placeholder="請輸入圖片連結">
                                <img class="img-fluid" :src="image">
                            </div>
                        </div>
                            <button class="btn btn-outline-primary btn-sm d-block w-100" 
                            @click="tempProduct.imagesUrl.push('')"
                            v-if="tempProduct.imagesUrl.length === 0 || tempProduct.imagesUrl[tempProduct.imagesUrl.length -1]">
                                新增圖片
                            </button>
                            <button  v-else class="btn btn-outline-danger btn-sm d-block w-100" @click="tempProduct.imagesUrl.pop()">
                                刪除圖片
                            </button>
                    </div>
                </div>
                <div class="col-sm-8">
                    <div class="mb-3">
                    <label for="title" class="form-label">標題</label>
                    <input id="title" type="text" class="form-control" placeholder="請輸入標題" v-model="tempProduct.title">
                    </div>

                    <div class="row">
                    <div class="mb-3 col-md-6">
                        <label for="category" class="form-label">分類</label>
                        <input id="category" type="text" class="form-control"
                                placeholder="請輸入分類" v-model="tempProduct.category">
                    </div>
                    <div class="mb-3 col-md-6">
                        <label for="price" class="form-label">單位</label>
                        <input id="unit" type="text" class="form-control" placeholder="請輸入單位" v-model="tempProduct.unit">
                    </div>
                    </div>

                    <div class="row">
                    <div class="mb-3 col-md-6">
                        <label for="origin_price" class="form-label">原價</label>
                        <input id="origin_price" type="number" min="0" class="form-control" placeholder="請輸入原價" v-model="tempProduct.origin_price">
                    </div>
                    <div class="mb-3 col-md-6">
                        <label for="price" class="form-label">售價</label>
                        <input id="price" type="number" min="0" class="form-control"
                                placeholder="請輸入售價" v-model="tempProduct.price">
                    </div>
                    </div>
                    <hr>

                    <div class="mb-3">
                    <label for="description" class="form-label">產品描述</label>
                    <textarea id="description" type="text" class="form-control"
                                placeholder="請輸入產品描述" v-model="tempProduct.description">
                    </textarea>
                    </div>
                    <div class="mb-3">
                    <label for="content" class="form-label">說明內容</label>
                    <textarea id="description" type="text" class="form-control"
                                placeholder="請輸入說明內容" v-model="tempProduct.content">
                    </textarea>
                    </div>
                    <div class="mb-3">
                    <div class="form-check">
                        <input id="is_enabled" class="form-check-input" type="checkbox"
                                :true-value="1" :false-value="0" v-model="tempProduct['is_enabled']">
                        <label class="form-check-label" for="is_enabled">是否啟用</label>
                    </div>
                    </div>
                </div>
                </div>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-outline-secondary" data-bs-dismiss="modal">
                取消
                </button>
                <button type="button" class="btn btn-primary" @click="updateProduct()">
                確認
                </button>
            </div>
            </div>
        </div>
    </div>
    <div id="delProductModal" ref="delProductModal" class="modal fade" tabindex="-1"
            aria-labelledby="delProductModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content border-0">
            <div class="modal-header bg-danger text-white">
                <h5 id="delProductModalLabel" class="modal-title">
                <span>刪除產品</span>
                </h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                是否刪除
                <strong class="text-danger">
                    {{ tempProduct.title }}
                </strong> 商品(刪除後將無法恢復)。
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-outline-secondary" data-bs-dismiss="modal">
                取消
                </button>
                <button type="button" class="btn btn-danger" @click="delProduct()">
                確認刪除
                </button>
            </div>
            </div>
        </div>
    </div>
</template>



<script>

import axios from 'axios'
import ProductModal from '../components/ProductModal.vue'

const { VITE_API, VITE_PATH } = import.meta.env

export default {
    data() {
        return {
            productsList: [],
            tempProduct: {
                imagesUrl: [],
                imageUrl:'',
            },
            productModal: null,
            delProductModal: null,
            isNew: false,
        }
    },
    methods: {
        //確認登入
        checkUser() {
            const token = document.cookie
                .split("; ")
                .find((row) => row.startsWith("hexToken="))
                ?.split("=")[1];
            axios.defaults.headers.common['Authorization'] = token;
            
            axios.post(`${VITE_API}/api/user/check`, null)
                .then(() => {
                    this.getProducts();
                })
                .catch(err => {
                    console.dir(err);
                })
        },
        //取得產品列表
        getProducts() {
            axios.get(`${VITE_API}/api/${VITE_PATH}/admin/products`)
            .then(res => {
                this.productsList = res.data.products;
                // console.log(res.data);
            })
            .catch(err => {
                console.dir(err.response.data);
            })
        },
        //查看產品細節
        // checkDetail(detail){
        //     this.tempProduct = {...detail};
        // },
        //彈跳視窗
        openModal(status, item) {
            if(status === 'new') {
                this.tempProduct = {
                    imagesUrl: [],
                }
                this.isNew = true;
                this.productModal.show();
            } else if (status === 'edit') {
                this.tempProduct = {...item}; //顯示已有產品資訊
                this.isNew = false;
                this.productModal.show();
                if(!Array.isArray(this.tempProduct.imagesUrl)) {
                    this.tempProduct.imagesUrl = [];
                }
            } else if (status === 'delete') {
                this.tempProduct = {...item}; 
                this.isNew = false;
                this.delProductModal.show();
            } 
        },
        //更新產品
        updateProduct() {
            let api = `${VITE_API}/api/${VITE_PATH}/admin/product`; // 新增
            let method ='post'; //方便切換的方法，此為新增
            if(!this.isNew) {
                api = `${VITE_API}/api/${VITE_PATH}/admin/product/${this.tempProduct.id}`;
                method = 'put';
            }
            axios[method](api, { data:this.tempProduct })
            .then(res => {
                // console.log(res.data);
                this.getProducts();
                this.productModal.hide();
            })
            .catch(err => {
                console.log(err);
            })
        },
        //刪除產品
        delProduct() {
            const api = `${VITE_API}/api/${VITE_PATH}/admin/product/${this.tempProduct.id}`; 
            axios.delete(api)
            .then(res => {
                // console.log(res);
                this.getProducts();
                this.delProductModal.hide();
            })
            .catch(err => {
                alert('刪除產品失敗');
                console.dir(err);
            })
        }
    },
    mounted() {
        this.checkUser();
        // console.log(this.$refs);
        this.productModal = new bootstrap.Modal(this.$refs.productModal)
        this.delProductModal = new bootstrap.Modal(this.$refs.delProductModal)
    },
    components: {
        ProductModal
    }
}

</script>



