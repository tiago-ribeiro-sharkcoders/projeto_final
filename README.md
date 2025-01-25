import os
import random
from datetime import datetime

# Função para gerar conteúdo aleatório com IA
def generate_ai_content():
    topics = [
        "Tecnologia",
        "Ciência",
        "Viagens",
        "Literatura",
        "Música",
        "Filosofia",
        "Esportes",
        "Culinária"
    ]

    content = {
        "Tecnologia": "A tecnologia está em constante evolução, trazendo avanços incríveis como inteligência artificial, computação quântica e conectividade global.",
        "Ciência": "A ciência continua a desvendar os mistérios do universo, desde a física de partículas até a biologia molecular, impactando diretamente nossa vida cotidiana.",
        "Viagens": "Viajar é uma das melhores formas de aprendizado. Conhecer novos lugares e culturas amplia nossa visão do mundo e nos conecta com diversas realidades.",
        "Literatura": "A literatura é um reflexo da sociedade, nos permitindo explorar a mente humana, passando por clássicos da literatura até novas tendências literárias contemporâneas.",
        "Música": "A música é uma linguagem universal que transcende barreiras culturais, com diferentes estilos capazes de tocar os corações das pessoas em qualquer parte do mundo.",
        "Filosofia": "A filosofia busca compreender a essência da vida, questões como moralidade, existência, liberdade e conhecimento são discutidas através dos tempos por grandes pensadores.",
        "Esportes": "O esporte é mais do que uma competição. Ele une pessoas, promove saúde física e mental e nos ensina importantes lições sobre perseverança e trabalho em equipe.",
        "Culinária": "A culinária é uma arte e ciência ao mesmo tempo, onde a combinação de sabores e texturas nos oferece uma experiência sensorial única, refletindo diferentes culturas."
    }

    topic = random.choice(topics)  # Escolhe um tópico aleatório
    return f"Tópico: {topic}\nConteúdo: {content[topic]}\n"  # Retorna o conteúdo relacionado ao tópico escolhido

# Função para organizar arquivos na pasta
def organize_files(folder_path):
    try:
        # Verificar se o caminho da pasta existe
        if not os.path.exists(folder_path):
            print("O caminho da pasta não existe!")
            return

        # Listar arquivos na pasta
        files = [f for f in os.listdir(folder_path) if os.path.isfile(os.path.join(folder_path, f))]

        # Organizar arquivos alfabeticamente (A-Z)
        files.sort()
        print("\nArquivos organizados alfabeticamente (A-Z):")
        for file in files:
            print(file)

        # Organizar arquivos por data de modificação (do mais recente ao mais antigo)
        files.sort(key=lambda x: os.path.getmtime(os.path.join(folder_path, x)), reverse=True)
        print("\nArquivos organizados do mais recente ao mais antigo:")
        for file in files:
            file_path = os.path.join(folder_path, file)
            mod_time = datetime.fromtimestamp(os.path.getmtime(file_path))
            print(f"{file} - Última modificação: {mod_time}")

    except Exception as e:
        print(f"Erro ao organizar arquivos: {e}")

# Função para fornecer ajuda ao usuário
def provide_help():
    print("\nOlá! Aqui está o que o programa pode fazer:")
    print("1. Organiza os arquivos em uma pasta de forma ordenada.")
    print("2. Você pode escolher organizar os arquivos alfabeticamente ou por data de modificação.")
    print("3. O programa também gera conteúdo com IA, escrevendo informações sobre tópicos variados.")
    print("4. Apenas digite o caminho da pasta onde deseja organizar os arquivos.")
    print("\nPara mais ajuda, basta digitar '333' novamente.")

# Função principal
def main():
    # Obter o nome do usuário do computador
    user_name = os.getlogin()

    # Sugerir o caminho padrão para o usuário
    suggested_path = f"C:/Users/{user_name}/"

    # Solicitar o caminho da pasta onde os arquivos serão organizados
    folder_path = input(f"Digite o caminho da pasta a ser organizada (padrão sugerido: {suggested_path}): ")

    # Caso o usuário digite "333", fornecemos ajuda
    if folder_path == "333":
        provide_help()
        return

    # Se o usuário não fornecer um caminho, usa o sugerido
    if not folder_path:
        folder_path = suggested_path

    # Gerar conteúdo com IA e salvar em um arquivo
    ai_content = generate_ai_content()
    ai_filename = "conteudo_gerado_com_ia.txt"
    ai_file_path = os.path.join(folder_path, ai_filename)

    # Escrever conteúdo no arquivo gerado
    try:
        with open(ai_file_path, 'w') as ai_file:
            ai_file.write(ai_content)
        print(f"\nConteúdo gerado com IA foi salvo no arquivo: {ai_filename}")
    except Exception as e:
        print(f"Erro ao salvar o conteúdo gerado com IA: {e}")

    # Organiza os arquivos da pasta
    organize_files(folder_path)

if __name__ == "__main__":
    main()
