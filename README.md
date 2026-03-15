# Nano Banana 2

Sistema de geração de imagens hiper-realistas usando o modelo **Nano Banana 2** (Gemini 3.1 Flash) através da API da **Kie.ai**.

Focado em fotos publicitárias de produtos com controle total sobre câmera, iluminação, textura e composição via prompts JSON estruturados.

## Estrutura do Projeto

```
├── prompts/          # Prompts JSON estruturados para cada imagem
├── images/           # Imagens geradas
├── scripts/          # Scripts Python para comunicação com a API
│   ├── generate_kie.py    # Gera imagem: envia prompt, faz polling, baixa resultado
│   └── get_kie_image.py   # Busca imagem de uma task já existente pelo taskId
├── skills/           # Definição de skill para assistentes IA
├── master_prompt_reference.md  # Guia completo do schema JSON de prompts
└── gemini.md         # Organização do projeto e workflow
```

## Setup

1. Crie um arquivo `.env` na raiz do projeto:
   ```
   KIE_AI_API_KEY=sua_chave_aqui
   ```

2. Instale as dependências:
   ```bash
   pip install requests
   ```

## Uso

### Gerar uma imagem

```bash
python scripts/generate_kie.py prompts/product_ads/seu_prompt.json images/product_ads/resultado.jpg "4:5"
```

- **Argumento 1:** Caminho do arquivo JSON com o prompt
- **Argumento 2:** Caminho de saída da imagem
- **Argumento 3 (opcional):** Aspect ratio (padrão: `auto`)

### Buscar imagem de uma task existente

```bash
python scripts/get_kie_image.py <taskId> images/output.jpg
```

## Formato do Prompt JSON

```json
{
  "prompt": "Descrição ultra-detalhada com matemática de câmera (85mm, f/1.8, ISO 100)...",
  "negative_prompt": "plastic skin, CGI, skin smoothing, beautification filters...",
  "image_input": ["url_da_imagem_de_referencia"],
  "api_parameters": {
    "resolution": "2K",
    "output_format": "jpg",
    "aspect_ratio": "4:5"
  },
  "settings": {
    "style": "documentary realism",
    "lighting": "natural golden hour",
    "camera_angle": "eye-level",
    "depth_of_field": "shallow",
    "quality": "high detail, unretouched skin"
  }
}
```

Consulte `master_prompt_reference.md` para o schema completo e boas práticas.
