# lesson_class

import pytest
import pytesseract
from PIL import Image
import enchant

class TestImg:

    def get_img(self):
        img = Image.open('/home/user/Desktop/python/image.jpg')
        text = pytesseract.image_to_string(img)
        return text


    def test_1(self):
        text = self.get_img()
        if len(text) <= 20:
            pytest.xfail("The Lenght Is Less 20")

    def test_2(self):
        text = self.get_img()
        if text[0] != text[0].title():
            pytest.fail("The Text Is Not Starting With Capital Letter")

    def test_3(self):
        text = self.get_img()
        sym_list = ["!","\"","#","$","%","&",",","“","”","\'","(",")","*","+","-",".",":",";","<","=",">","?","@","[","]","^","_","`","{","|","}","~"]
        for i in sym_list:
            if i in text:
                pytest.fail("There Is a Symbol in Text")

    def test_4(self):
        text = self.get_img()
        num_list = [1,2,3,4,5,6,7,8,9,0]
        for i in num_list:
            if str(i) in text:
                pytest.fail("There is a Number in Text")

    def test_5(self):
        text = self.get_img()
        sym_list = ["!","\"","#","$","%","&",",","“","”","\'","(",")","*","+","-",".",":",";","<","=",">","?","@","[","]","^","_","`","{","|","}","~"]
        for i in sym_list:
            if i in text:
                text = text.replace(i, "")
        txt = text.split()
        dictionary = enchant.Dict("en_US")
        for i in txt:
            if i == "Everything":
                if dictionary.check(i) is False:
                    pytest.fail( i + "The Text is Not in Enghish")



