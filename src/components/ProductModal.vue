<template>
    <div class="container">
        <div class="row">
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
                            <div class="mb-3">
                                <label for="imageUrl" class="form-label">輸入圖片網址</label>
                                <input type="text" class="form-control"
                                        placeholder="請輸入圖片連結">
                            </div>
                            <img class="img-fluid" src="" alt="">
                            </div>
                            <div>
                            <button class="btn btn-outline-primary btn-sm d-block w-100">
                                新增圖片
                            </button>
                            </div>
                            <div>
                            <button class="btn btn-outline-danger btn-sm d-block w-100">
                                刪除圖片
                            </button>
                            </div>
                        </div>
                        <div class="col-sm-8">
                            <div class="mb-3">
                            <label for="title" class="form-label">標題</label>
                            <input id="title" type="text" class="form-control" placeholder="請輸入標題">
                            </div>

                            <div class="row">
                            <div class="mb-3 col-md-6">
                                <label for="category" class="form-label">分類</label>
                                <input id="category" type="text" class="form-control"
                                        placeholder="請輸入分類">
                            </div>
                            <div class="mb-3 col-md-6">
                                <label for="price" class="form-label">單位</label>
                                <input id="unit" type="text" class="form-control" placeholder="請輸入單位">
                            </div>
                            </div>

                            <div class="row">
                            <div class="mb-3 col-md-6">
                                <label for="origin_price" class="form-label">原價</label>
                                <input id="origin_price" type="number" min="0" class="form-control" placeholder="請輸入原價">
                            </div>
                            <div class="mb-3 col-md-6">
                                <label for="price" class="form-label">售價</label>
                                <input id="price" type="number" min="0" class="form-control"
                                        placeholder="請輸入售價">
                            </div>
                            </div>
                            <hr>

                            <div class="mb-3">
                            <label for="description" class="form-label">產品描述</label>
                            <textarea id="description" type="text" class="form-control"
                                        placeholder="請輸入產品描述">
                            </textarea>
                            </div>
                            <div class="mb-3">
                            <label for="content" class="form-label">說明內容</label>
                            <textarea id="description" type="text" class="form-control"
                                        placeholder="請輸入說明內容">
                            </textarea>
                            </div>
                            <div class="mb-3">
                            <div class="form-check">
                                <input id="is_enabled" class="form-check-input" type="checkbox"
                                        :true-value="1" :false-value="0">
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
                        <button type="button" class="btn btn-primary">
                        確認
                        </button>
                    </div>
                    </div>
                </div>
                </div>
            <!-- <div class="col-md-6">
                <h2 class="mb-3">單一產品細節</h2>
                <template v-if="tempProduct.title">
                    <div class="card mb-3">
                        <img :src="tempProduct.imageUrl" class="card-img-top mb-3" :alt="主圖" />
                        <div class="card-body">
                            <h5 class="card-title">
                            {{  tempProduct.title }}
                            <span class="badge bg-primary ms-2">{{ tempProduct.category }}</span>
                            </h5>
                            <p class="card-text">商品描述：{{ tempProduct.description }}</p>
                            <p class="card-text">商品內容：{{ tempProduct.content  }}</p>
                            <div class="d-flex">
                                <p class="card-text me-2">{{ tempProduct.price }}</p>
                                <p class="card-text text-secondary"><del>{{ tempProduct.origin_price }}</del></p>
                                元 / {{ tempProduct.unit }}
                            </div>
                        </div>
                    </div>

                    <div class="row">
                        <div class="col-4 g-3" v-for="image in tempProduct.imagesUrl" :key="image">
                            <img :src="image" :alt="image" class="img-fluid object-fit-cover">
                        </div>
                    </div>
                </template>
                <p v-else class="text-secondary">請選擇一個商品查看</p>
            </div> -->
        </div>
    </div>

    
</template>






<script>
    export default {
        props: ['tempProduct']
    }
</script>

