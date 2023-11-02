import tkinter as tk
from tkinter import Label, Entry, Text, Button, filedialog
import os
from reportlab.lib.pagesizes import letter, portrait
from reportlab.lib.units import cm
from reportlab.platypus import SimpleDocTemplate, Paragraph
from reportlab.lib.styles import getSampleStyleSheet
from reportlab.platypus.doctemplate import LayoutError

def generate_pdf():
    font_path = font_path_entry.get()
    font_size = float(font_size_entry.get())
    pdf_text = pdf_text_entry.get("1.0", "end-1c")
    pdf_text = pdf_text.replace('\n', '<br/>')  # Substitua as quebras de linha por '<br/>'.

    left_margin = float(left_margin_entry.get()) * cm
    top_margin = float(top_margin_entry.get()) * cm
    right_margin = float(right_margin_entry.get()) * cm
    bottom_margin = float(bottom_margin_entry.get()) * cm

    output_directory = filedialog.askdirectory()
    
    if output_directory:
        user_defined_file_name = user_file_name_entry.get()
        
        # Adicione numeração no início do nome, antes da extensão ".pdf"
        if not user_defined_file_name:
            user_defined_file_name = "output"
        if not user_defined_file_name.endswith(".pdf"):
            user_defined_file_name += ".pdf"
        
        output_pdf_path = os.path.join(output_directory, user_defined_file_name)
        
        # Verificar a existência do arquivo e adicionar numeração
        file_name, file_extension = os.path.splitext(output_pdf_path)
        file_number = 1
        while os.path.exists(output_pdf_path):
            output_pdf_path = f"{file_name}_{file_number}{file_extension}"
            file_number += 1

        try:
            doc = SimpleDocTemplate(output_pdf_path, pagesize=portrait(letter),
                                    leftMargin=left_margin, rightMargin=right_margin,
                                    topMargin=top_margin, bottomMargin=bottom_margin)

            story = []
            styles = getSampleStyleSheet()
            style = styles["Normal"]

            text = Paragraph(pdf_text, style, encoding='utf-8')
            story.append(text)

            doc.build(story)

            result_label.config(text=f"PDF gerado com sucesso em: {output_pdf_path}")
        except LayoutError as e:
            result_label.config(text="Erro: O conteúdo é muito longo para caber em uma única página.")
    else:
        result_label.config(text="Nenhuma pasta selecionada.")

app = tk.Tk()
app.title("Gerador de PDF Personalizado")

font_path_label = Label(app, text="Caminho da Fonte (TTF):")
font_path_label.pack()
font_path_entry = Entry(app)
font_path_entry.pack()

font_size_label = Label(app, text="Tamanho da Letra:")
font_size_label.pack()
font_size_entry = Entry(app)
font_size_entry.pack()

left_margin_label = Label(app, text="Margem Esquerda (cm):")
left_margin_label.pack()
left_margin_entry = Entry(app)
left_margin_entry.pack()

top_margin_label = Label(app, text="Margem Superior (cm):")
top_margin_label.pack()
top_margin_entry = Entry(app)
top_margin_entry.pack()

right_margin_label = Label(app, text="Margem Direita (cm):")
right_margin_label.pack()
right_margin_entry = Entry(app)
right_margin_entry.pack()

bottom_margin_label = Label(app, text="Margem Inferior (cm):")
bottom_margin_label.pack()
bottom_margin_entry = Entry(app)
bottom_margin_entry.pack()

pdf_text_label = Label(app, text="Texto do PDF:")
pdf_text_label.pack()
pdf_text_entry = Text(app, height=10, width=40)
pdf_text_entry.pack()

user_file_name_label = Label(app, text="Nome do Arquivo (com ou sem extensão, ex: 'meuarquivo.pdf'):")
user_file_name_label.pack()
user_file_name_entry = Entry(app)
user_file_name_entry.pack()

generate_button = Button(app, text="Gerar PDF", command=generate_pdf)
generate_button.pack()

result_label = Label(app, text="")
result_label.pack()

app.mainloop()
