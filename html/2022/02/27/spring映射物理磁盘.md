# spring映射物理磁盘目录
实现WebMvcConfigurer接口的addResourceHandlers方法即可
```Java
@Configuration
public class FilePathConfig implements WebMvcConfigurer {
    @Value("${basePath}")
    private String filePath;
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/img/**").addResourceLocations("file:"+filePath);
    }
}
```