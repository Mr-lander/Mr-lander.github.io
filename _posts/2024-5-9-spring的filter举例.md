### spring的filter举例

```java
public class LoggingFilter implements Filter {
    // 省略其他方法

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        // 在处理请求之前记录日志
        System.out.println("LoggingFilter: Request received.");

        // 传递请求给下一个过滤器或目标资源
        chain.doFilter(request, response);

        // 在响应发送回客户端之后记录日志
        System.out.println("LoggingFilter: Response sent.");
    }
}

public class AuthenticationFilter implements Filter {
    // 省略其他方法

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        // 进行身份验证
        // 如果验证失败，则可以返回错误响应，或者直接结束请求

        // 如果验证通过，则传递请求给下一个过滤器或目标资源
        chain.doFilter(request, response);
    }
}

public class EncodingFilter implements Filter {
    // 省略其他方法

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        // 设置字符编码
        request.setCharacterEncoding("UTF-8");
        response.setCharacterEncoding("UTF-8");

        // 传递请求给下一个过滤器或目标资源
        chain.doFilter(request, response);
    }
}

```

注意看上面的两个doFilter不一样。

filterChain对象管理一组过滤器，当前过滤器执行结束后调用`filterChain`对象的doFilter方法交给下一个过滤器