const express = require("express");
const cors = require("cors");
const OpenAI = require("openai");

const app = express();

app.use(cors());
app.use(express.json());

const client = new OpenAI({
    apiKey: process.env.OPENAI_API_KEY
});

app.post("/ask", async (req, res) => {
    try {
        const question = req.body.question;

        if (!question) {
            return res.status(400).json({
                error: "Nenhuma questão enviada."
            });
        }

        const response = await client.responses.create({
            model: "gpt-5.6-luna",
            input:
`Você é um assistente de estudos.
Analise a questão abaixo e explique como chegar à resposta.
Não envie ou preencha automaticamente nenhuma atividade.

Questão:
${question}`
        });

        res.json({
            answer: response.output_text
        });

    } catch (error) {
        console.error(error);

        res.status(500).json({
            error: "Erro ao consultar a IA."
        });
    }
});

app.listen(3000, () => {
    console.log("MIKU SERVER rodando em http://localhost:3000");
});
