<div class="upload clear">
  <span>image_prefer</span>
   <vue-core-image-upload
      :class="['btn', 'btn-primary']"
      :crop="false"
      @imageuploaded="imageuploaded"
      input-of-file="file"
      :max-file-size="5242880"
      :url="uploadUrl">
      <img width="150" :src="formData.license" />
    </vue-core-image-upload>
 </div>



.upload{
  width: 100%;
  border-top: 1px solid #e1e1e1;
  padding: 0.3rem 0;
  span{
    width: 3rem;
    line-height: 0.8rem;
    font-size: 0.42rem;
    float: left;
    padding-left: 0.3rem;
    box-sizing: border-box;
  }
  .btn-primary{
    background-color: #16c2c2;
    color: #fff;
    padding: 0.3rem;
    height: 4rem;
    width: 5rem;
    float: left;
    img{
      width: 100%;
      height: 100%;
    }
  }
}
.g-core-image-upload-form{
  width: 100%!important;
  height: 100%!important;
}
