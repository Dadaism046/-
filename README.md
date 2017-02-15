# -*- coding: utf-8 -*-
"""
Created on Tue Dec  6 17:59:19 2016

@author: Dada
"""

from PyQt5.QtCore import QUrl
from PyQt5.QtWebEngineWidgets import QWebEngineView,QWebEnginePage
from PyQt5.QtWidgets import QApplication,QMainWindow,QAction

class MyWindow(QMainWindow):
    '''##############      初始化区            #########################'''
    def __init__(self,url):
        super(MyWindow,self).__init__()
        
        
        self.view = QWebEngineView(self)
        self.view.load(url) 
        
        self.setCentralWidget(self.view)
        
        viewMenu = self.menuBar().addMenu("&View")
        viewSourceAction = QAction("Click", self)
        viewSourceAction.triggered.connect(self.click)  
        viewMenu.addAction(viewSourceAction)
        
    def click(self):


        cede = '''baseForm.pageNumber.value = "2";baseForm.submit();
 '''
        code2 = '''function goPageHTML(id,pageCount)
{	    baseForm.pageNumber.value=5;
		var flag = true;
		baseForm.keyWords.value = encodeURIComponent(baseForm.keyWords.value);
		baseForm.contributor.value = encodeURIComponent(baseForm.contributor.value);
		baseForm.submit();

}'''
        code3 = '''document.getElementById('page_show').click()'''
        result = self.main_frame.evaluateJavaScript("%s" % code3)
        print(result)
        return result
        
if __name__ == '__main__':
    import sys
    app = QApplication(sys.argv)
    url = QUrl("http://oa.zs.zj.com.yc/zsportal/portal/more.psml?MORE_IDS=sjcms_8&TEMPLATE=cmsMore")
    #url = QUrl(r"C:\Users\Dada\DesktopC:\Users\Dada\Desktop\htmlyc.htm")
    browser = MyWindow(url)
    browser.show()
    

