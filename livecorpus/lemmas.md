Т.к. файл с разметкой очень большой, у меня не получилось разметить столбей токенов,попробовала  на части, успешнот прошло проверку,могу предположить, подходит и для всего файла:
from pymystem3 import Mystem

mystem = Mystem()

with open('words_Irkutsk_eam2007-1.txt', 'r', encoding='utf-8') as f:
    token = f.read().split()

text = ' '.join(token)
analysis = mystem.analyze(text)

def format_gramms(gr):
    parts = gr.split('=')
    pos_features = parts[0].split(',')
    if len(parts) > 1:
        case_nums = parts[1]
        return ','.join(pos_features) + '=' + case_nums
    else:
        return ','.join(pos_features) + '='

for token_info in analysis:
    token = token_info['text']
    if 'analysis' in token_info and token_info['analysis']:
        lexeme = token_info['analysis'][0]['lex']
        gramm = token_info['analysis'][0]['gr']
        gramm_formatted = format_gramms(gramm)
         print(f"{token} {lexeme}{gramm_formatted}")
    else:
        print(f"{token}=")
  Далее нужно добавить время, сделать это тоже можно с помощью регулярного выражения:
  ([^\t]+)\t([^\t]+)\t([^\t]+)
