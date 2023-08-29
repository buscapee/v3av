import sys
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QVBoxLayout, QLabel, QInputDialog, QMessageBox, QLineEdit
from threading import Thread
from PyQt5.QtGui import QFont, QIcon, QPixmap
import keyboard
import time
import webbrowser
import requests
from PyQt5.QtCore import Qt


class PaginaInicial(QWidget):
    def __init__(self, parent=None):
        super().__init__(parent)
        self.setWindowTitle("AVerse")
        self.setFixedSize(210, 200)
        self.setWindowFlags(self.windowFlags() | Qt.WindowStaysOnTopHint)
        self.setWindowIcon(QIcon("assets/dme.ico"))
        
        layout = QVBoxLayout()

        label_fundo = QLabel()
        pixmap_fundo = QPixmap('assets/dmelogo.png')
        width = 100  
        label_fundo.setPixmap(pixmap_fundo.scaledToWidth(width))
        label_fundo.setAlignment(Qt.AlignCenter)
        
        layout.addWidget(label_fundo)

        labeldme_texto = QLabel("POLÍCIA DME")
        labeldme_texto.setAlignment(Qt.AlignCenter)
        labeldme_texto.setFont(QFont("Arial", 11))
        labeldme_texto.setStyleSheet("background-color: transparent;")
        layout.addWidget(labeldme_texto)

        label_texto = QLabel("AutoVerse v2 - 2023")
        label_texto.setAlignment(Qt.AlignCenter)
        label_texto.setFont(QFont("Arial", 9))
        label_texto.setStyleSheet("background-color: transparent;")
        layout.addWidget(label_texto)
        
        button = QPushButton("Abrir AutoVerse")
        button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #006633, stop: 1 #004D26);
                color: white;
                font-size: 14px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }
            
            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #004D26, stop: 1 #006633);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        button.clicked.connect(self.redirecionar)
        layout.addWidget(button)
        
        self.setLayout(layout)
    
    def redirecionar(self):
        self.hide()
        janela_principal.show()

class FrasesApp(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("[CS] AVerse")
        self.setFixedSize(230, 380)
        self.setWindowFlags(self.windowFlags() | Qt.WindowStaysOnTopHint)
        self.setWindowIcon(QIcon("assets/dme.ico"))

        
        layout = QVBoxLayout()
        
        trecho0_button = QPushButton("[CS] INS", self)
        trecho0_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #006633, stop: 1 #004D26);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #004D26, stop: 1 #006633);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        trecho0_button.clicked.connect(self.start_trecho0)
        layout.addWidget(trecho0_button)
        
        trecho1_button = QPushButton("[CS] CSO", self)
        trecho1_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #006633, stop: 1 #004D26);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #004D26, stop: 1 #006633);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        trecho1_button.clicked.connect(self.start_trecho1)
        layout.addWidget(trecho1_button)
        
        trecho2_button = QPushButton("[CS] CAS", self)
        trecho2_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #006633, stop: 1 #004D26);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #004D26, stop: 1 #006633);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        trecho2_button.clicked.connect(self.start_trecho2)
        layout.addWidget(trecho2_button)
        
        trecho3_button = QPushButton("[CS] PRO", self)
        trecho3_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #006633, stop: 1 #004D26);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #004D26, stop: 1 #006633);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        trecho3_button.clicked.connect(self.start_trecho3)
        layout.addWidget(trecho3_button)
        
        trecho4_button = QPushButton("[CS] CAP", self)
        trecho4_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #006633, stop: 1 #004D26);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #004D26, stop: 1 #006633);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        trecho4_button.clicked.connect(self.check_password_trecho4)
        layout.addWidget(trecho4_button)
        
        trecho5_button = QPushButton("[CS] ADM", self)
        trecho5_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #006633, stop: 1 #004D26);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #004D26, stop: 1 #006633);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        trecho5_button.clicked.connect(self.check_password_trecho5)
        layout.addWidget(trecho5_button)
        
        site_button = QPushButton("System", self)
        site_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #464c44, stop: 1 #2d2e2d);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #2d2e2d, stop: 1 #464c44);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        site_button.clicked.connect(self.open_website)
        layout.addWidget(site_button)
        
        youtube_button = QPushButton("Fórum", self)
        youtube_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #464c44, stop: 1 #2d2e2d);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #2d2e2d, stop: 1 #464c44);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        youtube_button.clicked.connect(self.open_youtube)
        layout.addWidget(youtube_button)
        
        support_button = QPushButton("Suporte", self)
        support_button.setStyleSheet("""
            QPushButton {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #464c44, stop: 1 #2d2e2d);
                color: white;
                font-size: 13px;
                padding: 8px 13px;
                border-radius: 5px;
                border: none;
            }

            QPushButton:hover {
                background: qlineargradient(x1: 0, y1: 0, x2: 0, y2: 1, stop: 0 #2d2e2d, stop: 1 #464c44);
            }

            QPushButton:pressed {
                padding-left: 14px;
                padding-top: 10px;
            }
        """)
        support_button.clicked.connect(self.open_support)
        layout.addWidget(support_button)
        
        credits_label = QLabel(" Gestão Técnica Development")
        credits_label.setAlignment(Qt.AlignCenter)
        credits_label.setFont(QFont("Arial", 8))
        layout.addWidget(credits_label)

        self.info_label = QLabel(self)
        self.info_label.setText("Clique na aula para iniciar")
        self.info_label.setAlignment(Qt.AlignCenter)
        self.info_label.setFont(QFont("Arial", 8))
        layout.addWidget(self.info_label)
        
        self.setLayout(layout)
        

    def carregar_frases_de_site(self, url):
        try:
            response = requests.get(url)
            response.raise_for_status()  
            frases = response.text.split('\n')
            return frases
        except requests.exceptions.RequestException as e:
            print("Erro ao carregar as frases:", e)
            return []

    def carregar_frases_do_github(self):
        url_frases = "https://raw.githubusercontent.com/buscapee/autoversecs/frases-update/csnovo.txt"
        
        try:
            response = requests.get(url_frases)
            response.raise_for_status()  # Lança um erro se a solicitação não for bem-sucedida
            frases = response.text.splitlines()
            return frases
        except requests.exceptions.RequestException as e:
            print("Erro ao carregar frases:", e)
            return []

    def start_trecho0(self):
        self.info_label.setText("INS iniciado, vá para o Habbo.")
        frases = self.carregar_frases_do_github()  
        thread = Thread(target=self.send_phrases, args=(frases,))
        thread.start()
    
    def start_trecho1(self):
        self.info_label.setText("CSO iniciado, vá para o Habbo.")
        frases = [
            "Gritar! Olá, sou o supervisor responsável pelo seu Curso de Segurança Operacional.",
            "Gritar! Peço que mantenha a postura até o final da aula. Em caso de dúvidas, acene.",
            "Sussurrar null [Boa aula, Supervisor! Estamos direcionando você para o System.]"
        ]
        
        thread = Thread(target=self.send_phrases, args=(frases,))
        thread.start()
    
    def start_trecho2(self):
        self.info_label.setText("CAS iniciado, vá para o Habbo.")
        frases = [
            "Gritar! Olá, Sargento! Eu sou o supervisor responsável pela sua aula.",
            "Gritar! e ficarei responsável pelo seu Curso de Aperfeiçoamento de Sargentos.",
            "Sussurrar null [Boa aula, Supervisor! Estamos direcionando você para o System.]"
        ]
        
        thread = Thread(target=self.send_phrases, args=(frases,))
        thread.start()
    
    def start_trecho3(self):
        self.info_label.setText("PRO iniciado, vá para o Habbo.")
        frases = [
            "Gritar! Olá, Subtenente! Sou o supervisor responsável pela sua Aula para Promotor.",
            "Gritar! Nessa aula verá informações importantes para realizar uma promoção corretamente.",
            "Gritar! Peço que mantenha a postura até o final da aula. Em caso de dúvidas, acene.",
            "Sussurrar null [Boa aula, Supervisor! Estamos direcionando você para o System.]"
        ]
        
        thread = Thread(target=self.send_phrases, args=(frases,))
        thread.start()
    
    def check_password_trecho4(self):
        password, ok = QInputDialog.getText(self, "Senha", "Digite a senha:", QLineEdit.Password)
        if ok and password == "cscap@":
            self.start_trecho4()
        else:
            QMessageBox.warning(self, "Error", "Senha incorreta. Tente novamente.")
    
    def check_password_trecho5(self):
        password, ok = QInputDialog.getText(self, "Senha", "Digite a senha:", QLineEdit.Password)
        if ok and password == "cs/min@":
            self.start_trecho5()
        else:
            QMessageBox.warning(self, "Error", "Senha incorreta. Tente novamente.")
    
    def start_trecho4(self):
        self.info_label.setText("CAP iniciado, vá para o Habbo.")
        frases = [
            "Gritar! Saudações, Supervisor! Parabéns pela sua aprovação no teste de admissão.",
            "Gritar! Bem-vindo ao Centro de Supervisão.",
            "Gritar! Eu sou Capacitador e estarei passando-lhe os detalhes restantes",
            "Sussurrar null [Boa aula, Capacitador! Estamos direcionando você para o System.]"
        ]
        
        thread = Thread(target=self.send_phrases, args=(frases,))
        thread.start()
    
    def start_trecho5(self):
        self.info_label.setText("ADM iniciado, vá para o Habbo.")
        frases = [
            "Gritar! Olá, militar! Seja bem-vindo ao teste admissional do Centro de Supervisão.",
            "Gritar! Aqui, você irá aprender tudo sobre o Centro de Supervisão e suas responsabilidades.",
            "Gritar! Peço que fique em silêncio e atento. Caso tenha dúvidas, basta acenar.",
            "Sussurrar null [Boa admissão, Ministro! Estamos direcionando você para o System.]"

        ]
        
        thread = Thread(target=self.send_phrases, args=(frases,))
        thread.start()
    
    def send_phrases(self, frases):
        def on_key_press(event):
            if event.name == "tab":
                try:
                    frase = next(frases_generator)
                    keyboard.write(frase)
                    keyboard.press("enter")
                    keyboard.release("enter")
                    if frase == frases[-1]:
                        webbrowser.open("https://dme.systemhb.net/funcao/centro-de-supervisao/documentos")
                        self.reset_info_label()
                except StopIteration:
                    keyboard.unhook_all()  
                    self.reset_info_label()
    
        frases_generator = iter(frases)
        keyboard.on_press_key("tab", on_key_press)

    def reset_info_label(self):
        self.info_label.setText("Clique na aula para iniciar")


    def open_website(self):
        webbrowser.open("https://dme.systemhb.net/funcao/centro-de-supervisao/documentos")
    
    def open_youtube(self):
        webbrowser.open("https://policiadme.forumeiros.com/f125-cs-scripts")
    
    def open_support(self):
        webbrowser.open("https://docs.google.com/forms/d/e/1FAIpQLSeNAeJOC_MzgJRsIA8iNimPuAwJ4mNgJMSTVqlxPOQhti14Ww/viewform")


    def closeEvent(self, event):
        QApplication.quit() 


if __name__ == "__main__":
    app = QApplication(sys.argv)
    app.setStyleSheet("""
        QWidget {
            background-color: #f0f0f0;
        }
    """)
    pagina_inicial = PaginaInicial()
    janela_principal = FrasesApp()

    # Carrega as frases do GitHub
    frases = janela_principal.carregar_frases_do_github()
    
    pagina_inicial.show()
    
    sys.exit(app.exec_())
