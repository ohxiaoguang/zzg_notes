依赖
```

		<dependency>
		<groupId>com.itextpdf</groupId>
		<artifactId>itextpdf</artifactId>
		<version>5.5.1</version>
	</dependency>
	  <dependency>
            <groupId>com.itextpdf.tool</groupId>
            <artifactId>xmlworker</artifactId>
            <version>5.5.9</version>
    </dependency>
    <dependency>
        <groupId>com.itextpdf</groupId>
        <artifactId>kernel</artifactId>
        <version>7.2.0</version>
    </dependency>
    <dependency>
        <groupId>com.itextpdf</groupId>
        <artifactId>font-asian</artifactId>
        <version>7.2.0</version>
    </dependency>
    
     <dependency>
	      <groupId>com.aspose</groupId>
	      <artifactId>words</artifactId>
	      <version>18.6-jdk16-crack</version>
	    </dependency>
```



```
import com.aspose.words.License;
import com.aspose.words.SaveFormat;
import com.itextpdf.kernel.pdf.PdfDocument;
import com.itextpdf.text.pdf.PdfReader;
import com.itextpdf.kernel.pdf.canvas.parser.PdfTextExtractor;
import com.itextpdf.text.BadElementException;

import com.itextpdf.text.Document;
import com.itextpdf.text.DocumentException;
import com.itextpdf.text.Image;
import com.itextpdf.text.Rectangle;
import com.itextpdf.text.pdf.PdfCopy;
import com.itextpdf.text.pdf.PdfImportedPage;
import com.itextpdf.text.pdf.PdfWriter;

import java.awt.image.BufferedImage;
import java.io.BufferedOutputStream;
import java.io.ByteArrayInputStream;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.MalformedURLException;
import java.net.URL;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;

import javax.imageio.ImageIO;

public class PdfUtils {
	
	/**
	 * 统计pdf字数的工具
	 *
	 */
    public static Integer countText(String fileName) throws IOException {
        try {
        	com.itextpdf.kernel.pdf.PdfReader reader = new com.itextpdf.kernel.pdf.PdfReader(fileName);
            return countText(reader);
        } catch (IOException e) {
        	System.out.println("打开pdf失败，文件名:"+ fileName+e);
            throw e;
        }
    }

    /**
     * 统计pdf字数的工具
     *
     */
    public static Integer countText(InputStream inputStream) throws IOException {
        try {
        	com.itextpdf.kernel.pdf.PdfReader reader = new com.itextpdf.kernel.pdf.PdfReader(inputStream);
            return countText(reader);
        } catch (IOException e) {
        	System.out.println("使用流打开pdf失败"+ e);
            throw e;
        }
    }

    /**
     * 统计pdf字数的工具
     *
     */
    public static Integer countText(com.itextpdf.kernel.pdf.PdfReader reader) {
        try {
            int characterCount = 0;

            PdfDocument pdfDoc = new PdfDocument(reader);
            // get the number of pages in PDF
            int noOfPages = pdfDoc.getNumberOfPages();
            System.out.println("Extracted content of PDF---- ");
            for (int i = 1; i <= noOfPages; i++) {
                // Extract content of each page
                String contentOfPage = PdfTextExtractor.getTextFromPage(pdfDoc.getPage(i));
                contentOfPage = contentOfPage.replaceAll("\\p{C}", "").replaceAll(" ", "");
                characterCount += contentOfPage.length();
                System.out.println(contentOfPage);
                System.out.println("这页几个字：" + contentOfPage.length());
            }
            pdfDoc.close();
            System.out.println("文档总共" + characterCount + "个字");
            return characterCount;
        } finally {
            try {
                if (reader != null) {
                    reader.close();
                }
            } catch (IOException e) {
                // do noting
            }
        }
    }
    
    /**
     * 图片转pdf
     * @param imagePath
     * @param pdfPath
     */
    public static void imgToPdf(String imagePath,String pdfPath){
    	try {

        	BufferedImage img = ImageIO.read(new File(imagePath));

        	FileOutputStream fos = new FileOutputStream(pdfPath);

        	Document doc = new Document(null, 0, 0, 0, 0);

        	doc.setPageSize(new Rectangle(img.getWidth(), img.getHeight()));

        	Image image = Image.getInstance(imagePath);

        	PdfWriter.getInstance(doc, fos);

        	doc.open();

        	doc.add(image);

        	doc.close();

        } catch (IOException e) {
        	e.printStackTrace();

        } catch (BadElementException e) {
        	e.printStackTrace();

        } catch (DocumentException e) {
        	e.printStackTrace();

        }

    }
    
    /**
     * 图片转pdf
     * @param url
     * @param pdfPath
     */
    public static void imgToPdf(URL url,String pdfPath){
    	try {

        	BufferedImage img = ImageIO.read(url);

        	FileOutputStream fos = new FileOutputStream(pdfPath);

        	Document doc = new Document(null, 0, 0, 0, 0);

        	doc.setPageSize(new Rectangle(img.getWidth(), img.getHeight()));

        	Image image = Image.getInstance(url);

        	PdfWriter.getInstance(doc, fos);

        	doc.open();

        	doc.add(image);

        	doc.close();

        } catch (IOException e) {
        	e.printStackTrace();

        } catch (BadElementException e) {
        	e.printStackTrace();

        } catch (DocumentException e) {
        	e.printStackTrace();

        }

    }
    
    
    /**
     * word转pdf
     * @param url
     * @param pdfPath
     */
    public static void wordToPdf(URL url,String pdfPath){
    	OutputStream out = null;
		try {
			String s = "<License><Data><Products><Product>Aspose.Total for Java</Product><Product>Aspose.Words for Java</Product></Products><EditionType>Enterprise</EditionType><SubscriptionExpiry>20991231</SubscriptionExpiry><LicenseExpiry>20991231</LicenseExpiry><SerialNumber>8bfe198c-7f0c-4ef8-8ff0-acc3237bf0d7</SerialNumber></Data><Signature>sNLLKGMUdF0r8O1kKilWAGdgfs2BvJb/2Xp8p5iuDVfZXmhppo+d0Ran1P9TKdjV4ABwAgKXxJ3jcQTqE/2IRfqwnPf8itN8aFZlV3TJPYeD3yWE7IT55Gz6EijUpC7aKeoohTb4w2fpox58wWoF3SNp6sK6jDfiAUGEHYJ9pjU=</Signature></License>";
			ByteArrayInputStream is = new ByteArrayInputStream(s.getBytes());
			License license = new License();
			license.setLicense(is);
			com.aspose.words.Document document = new com.aspose.words.Document(url.openStream());
			out = new FileOutputStream(new File(pdfPath));
			document.save(out,SaveFormat.PDF);
		} catch (Exception e) {
			e.printStackTrace();
		}finally{
		  try {
                if (out != null) {
                	out.close();
                }
            } catch (IOException e) {
                // do noting
            }
		}
    }
    
    /**
     * word转pdf
     * @param url
     * @param pdfPath
     */
    public static void wordToPdf(String wordPath,String pdfPath){
    	OutputStream out = null;
		try {
			String s = "<License><Data><Products><Product>Aspose.Total for Java</Product><Product>Aspose.Words for Java</Product></Products><EditionType>Enterprise</EditionType><SubscriptionExpiry>20991231</SubscriptionExpiry><LicenseExpiry>20991231</LicenseExpiry><SerialNumber>8bfe198c-7f0c-4ef8-8ff0-acc3237bf0d7</SerialNumber></Data><Signature>sNLLKGMUdF0r8O1kKilWAGdgfs2BvJb/2Xp8p5iuDVfZXmhppo+d0Ran1P9TKdjV4ABwAgKXxJ3jcQTqE/2IRfqwnPf8itN8aFZlV3TJPYeD3yWE7IT55Gz6EijUpC7aKeoohTb4w2fpox58wWoF3SNp6sK6jDfiAUGEHYJ9pjU=</Signature></License>";
			ByteArrayInputStream is = new ByteArrayInputStream(s.getBytes());
			License license = new License();
			license.setLicense(is);
			com.aspose.words.Document document = new com.aspose.words.Document(wordPath);
			out = new FileOutputStream(new File(pdfPath));
			document.save(out,SaveFormat.PDF);
		} catch (Exception e) {
			e.printStackTrace();
		}finally{
			try {
                if (out != null) {
                	out.close();
                }
            } catch (IOException e) {
                // do noting
            }
		}
    }
    
    
    /**
     * 合并本地PDF文件
     * @param sourceFilePaths 需要合并的PDF文件路径列表
     * @param destFilePath 合并后的新文件
     */
    public static void mergeLocalPdfFile(List<String> sourceFilePaths, String destFilePath) {
        if (sourceFilePaths == null || sourceFilePaths.isEmpty() || destFilePath == null) {
            return;
        }

        Document document = null;
        PdfCopy copy = null;
        OutputStream os = null;
        try {
            // 创建合并后的新文件的目录
            Path dirPath = Paths.get(destFilePath.substring(0, destFilePath.lastIndexOf(File.separator)));
            Files.createDirectories(dirPath);

            os = new BufferedOutputStream(new FileOutputStream(new File(destFilePath)));
            document = new Document(new PdfReader(sourceFilePaths.get(0)).getPageSize(1));
            copy = new PdfCopy(document, os);
            document.open();
            for (String sourceFilePath : sourceFilePaths) {
                // 如果PDF文件不存在，则跳过
                if (!new File(sourceFilePath).exists()) {
                    continue;
                }

                // 读取需要合并的PDF文件
                PdfReader reader = new PdfReader(sourceFilePath);
                // 获取PDF文件总页数
                int n = reader.getNumberOfPages();
                for (int j = 1; j <= n; j++) {
                    document.newPage();
                    PdfImportedPage page = copy.getImportedPage(reader, j);
                    copy.addPage(page);
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (copy != null) {
                try {
                    copy.close();
                } catch (Exception ex) {
                    /* ignore */
                }
            }
            if (document != null) {
                try {
                    document.close();
                } catch (Exception ex) {
                    /* ignore */
                }
            }
            if (os != null) {
                try {
                    os.close();
                } catch (Exception ex) {
                    /* ignore */
                }
            }
        }
    }
    
    
    /**
     * 合并PDF文件
     * @param sourceFilePaths 需要合并的PDF文件
     * @param destFilePath 合并后的新文件
     */
    public static void mergePdfFile(List<PdfReader> sourcePdfFiles, String destFilePath) {
        if (sourcePdfFiles == null || sourcePdfFiles.isEmpty() || destFilePath == null) {
            return;
        }

        Document document = null;
        PdfCopy copy = null;
        OutputStream os = null;
        try {
            // 创建合并后的新文件的目录
            Path dirPath = Paths.get(destFilePath.substring(0, destFilePath.lastIndexOf(File.separator)));
            Files.createDirectories(dirPath);

            os = new BufferedOutputStream(new FileOutputStream(new File(destFilePath)));

            document = new Document(sourcePdfFiles.get(0).getPageSize(1));

            copy = new PdfCopy(document, os);
            document.open();
            for (PdfReader sourceFile : sourcePdfFiles) {
            	try{
                    // 获取PDF文件总页数
                    int n = sourceFile.getNumberOfPages();
                    for (int j = 1; j <= n; j++) {
                        document.newPage();
                        PdfImportedPage page = copy.getImportedPage(sourceFile, j);
                        copy.addPage(page);
                    }
                } catch (Exception e) {
                	e.printStackTrace();
                }

            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (copy != null) {
                try {
                    copy.close();
                } catch (Exception ex) {
                    /* ignore */
                }
            }
            if (document != null) {
                try {
                    document.close();
                } catch (Exception ex) {
                    /* ignore */
                }
            }
            if (os != null) {
                try {
                    os.close();
                } catch (Exception ex) {
                    /* ignore */
                }
            }
        }
    }
    
    
    
    

//    public static void main(String[] args) throws IOException {
//        //String testPdf = "C:\\Users\\Administrator\\Downloads\\330000220720836779868_音像_2022-07-22 (1).pdf";
//        String testPdf = "C:\\Users\\Administrator\\Desktop\\ceshi.txt";
//    	countText(testPdf);
//    }
    
    
    public static void main(String[] args) throws MalformedURLException {
//    	String pdf1 = "C:\\Users\\Administrator\\Desktop\\test1.png";
//
//    	String pdfPath = "C:\\Users\\Administrator\\Desktop\\test1.pdf";
////    	
//    	imgToPdf(new URL("http://223.4.75.77:8092/sfjd/upload/202204/736efc81e9804e358c9781fb881697da_%E4%BF%9E%E5%85%8B%E5%BC%BA-2%E5%AF%B8%E5%85%8D%E5%86%A0%E8%93%9D%E5%BA%95%E8%AF%81%E4%BB%B6%E7%85%A7.jpg")
//    			,pdfPath);
//    	
    	
//		try {
//			String url = "http://223.4.75.77:8092/sfjd/upload/202112/ba628d719f994a5188bbcc9a0b627197_司法鉴定许可证正、副本.pdf";
//			url = url.substring(0, url.lastIndexOf("/") + 1) + URLEncoder.encode(url.substring(url.lastIndexOf("/") + 1), "UTF-8");
//			System.out.println(url);
//			List<PdfReader> list = Arrays.asList(
//					new PdfReader("C:\\Users\\Administrator\\Desktop\\test2.pdf"),
//					new PdfReader(new URL(url))
//					);
//			
//			mergePdfFile(list,"C:\\Users\\Administrator\\Desktop\\test3.pdf");
////			
////			OssUploadUtil ossUploadUtil = new OssUploadUtil();
////			ossUploadUtil.MultipartUpload(OssUploadUtil.getBucketName(), "upload/202111/test3.pdf", new File("C:\\Users\\Administrator\\Desktop\\test3.pdf"));
////			
//		} catch (IOException e) {
//			// TODO Auto-generated catch block
//			e.printStackTrace();
//		}
    	
//    	String url = "/D:/Code/dev/sfjd20211222/eclipse/.metadata/.plugins/org.eclipse.wst.server.core/tmp3/wtpwebapps/was-web/WEB-INF/classes/app/page/doc/attr_temp/40ee08664ce14a09b755317c922fb7ef_材料归档测试.pdf";
//    	int i = url.lastIndexOf(File.separator);
//    	String s = url.substring(0,i);
//    	System.out.println(s);
    	
//    	String url = "http://223.4.75.77:8092/sfjd/upload/202111/726dc2ce2324446bb67f0f4286b976e4_%E8%81%8C%E7%A7%B0.docx";
//    	try {
//    		byte[] respBytes = docxToPdf(new URL(url).openStream());
//			
//			if(respBytes != null){
//			   String filepath ="C:\\Users\\Administrator\\Desktop\\test4.pdf";
//			   File file  = new File(filepath);
//			   if(file.exists()){
//			      file.delete();
//			   }
//			   FileOutputStream fos = new FileOutputStream(file);
//			   fos.write(respBytes,0,respBytes.length);
//			   fos.flush();
//			   fos.close();
//			}
//		} catch (IOException e) {
//			// TODO Auto-generated catch block
//			e.printStackTrace();
//		}
    	
    	
    	// TODO Auto-generated method stub
//    			String docPath ="C:\\Users\\Administrator\\Desktop\\726dc2ce2324446bb67f0f4286b976e4_职称.docx";
//    			String savePath="C:\\Users\\Administrator\\Desktop\\test6.pdf";
//    	    	String url = "http://223.4.75.77:8092/sfjd/upload/202111/726dc2ce2324446bb67f0f4286b976e4_%E8%81%8C%E7%A7%B0.docx";


    	
    }
}
```