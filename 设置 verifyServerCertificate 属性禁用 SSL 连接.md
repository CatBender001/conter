如何设置 verifyServerCertificate 属性为 false 来禁用 SSL 连接？

1.在代码中创建一个 SSL 连接

2.调用 SSL 连接对象的 setVerifyServerCertificate(false) 方法，将 verifyServerCertificate 属性设置为 false

3.连接到 SSL 服务器

4.示例代码如下：

    import java.io.IOException;
    import java.net.Socket;
    import java.security.SecureRandom;
    import javax.net.ssl.SSLContext;
    import javax.net.ssl.SSLSocket;
    import javax.net.ssl.TrustManager;
    import javax.net.ssl.X509TrustManager;
    
    public class DisableSSLCertificateCheck {
    
      public static void main(String[] args) throws IOException {
          String server = "example.com";
          int port = 443;
      SSLContext sslContext = SSLContext.getInstance("TLS");
      sslContext.init(null, new TrustManager[]{new X509TrustManager() {
          @Override
          public void checkClientTrusted(java.security.cert.X509Certificate[] chain,
                                         String authType) {
          }
    
          @Override
          public void checkServerTrusted(java.security.cert.X509Certificate[] chain,
                                         String authType) {
          }
    
          @Override
          public java.security.cert.X509Certificate[] getAcceptedIssuers() {
              return null;
          }
      }}, new SecureRandom());
    
      Socket socket = sslContext.getSocketFactory().createSocket(server, port);
      SSLSocket sslSocket = (SSLSocket) socket;
    
      sslSocket.setVerifyServerCertificate(false);
    
      // connect to the SSL server
      sslSocket.startHandshake();
      }
    }
  