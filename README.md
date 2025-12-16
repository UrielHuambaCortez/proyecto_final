import discord
import random
from discord.ext import commands

# === Inicio bot ===
intents = discord.Intents.default()
intents.message_content = True

bot = commands.Bot(command_prefix='$', intents=intents)

# Guardará el índice de la última pregunta enviada
bot.indice_pregunta = None

# === LISTA DE PREGUNTAS ===
preguntas = [
    "¿Cuál es el gas principal responsable del efecto invernadero?",
    "¿Qué porcentaje del planeta está cubierto de agua?",
    "¿Qué recurso natural es renovable?",
    "¿Cómo se llama el proceso por el cual las plantas producen oxígeno?",
    "¿Cuál es la capa que protege la Tierra de los rayos UV?",
]

# === LISTA DE RESPUESTAS (mismo orden que las preguntas) ===
respuestas = [
    "El dióxido de carbono (CO2).",
    "Aproximadamente el 70%.",
    "La energía solar.",
    "Fotosíntesis.",
    "La capa de ozono.",
]


# === DATOS CURIOSOS ===
datos_curiosos = [
    "Una sola botella de plástico tarda más de 400 años en descomponerse.",
    "Los árboles pueden comunicarse entre sí mediante señales químicas bajo tierra.",
    "Las abejas son responsables de la polinización del 70% de los cultivos del mundo.",
    "El 20% del oxígeno del mundo proviene del Amazonas.",
    "Reciclar una lata de aluminio ahorra energía suficiente para encender un televisor durante 3 horas.",
]

# === ECO TIPS ===
eco_tips = [
    "Apaga las luces cuando no las estés usando.",
    "Reduce el plástico usando botellas y bolsas reutilizables.",
    "Separa tus residuos en orgánicos, reciclables y no reciclables.",
    "Usa bicicleta o camina cuando puedas para reducir contaminación.",
    "Ahorra agua cerrando el grifo al lavarte los dientes.",
]

# === FRASES INSPIRADORAS ===
frases_inspiradoras = [
    "La Tierra no es una herencia de nuestros padres, sino un préstamo de nuestros hijos.",
    "Quien planta un árbol, planta esperanza.",
    "La naturaleza es el arte de Dios.",
    "No heredamos el planeta de nuestros antepasados, lo tomamos prestado de nuestros hijos.",
    "Cada pequeño acto cuenta cuando se trata de cuidar la Tierra.",
]

# === CURIOSIDADES DE ANIMALES ===
curiosidades_animales = [
    "Los delfines pueden reconocerse en un espejo, demostrando autoconciencia.",
    "Los colibríes son los únicos pájaros capaces de volar hacia atrás.",
    "Los elefantes pueden reconocer emociones humanas.",
    "Los pulpos tienen tres corazones y sangre azul.",
    "Las tortugas marinas pueden vivir más de 100 años.",
]

# === DATOS SOBRE CONTAMINACIÓN ===
datos_contaminacion = [
    "Cada año se producen más de 300 millones de toneladas de plástico.",
    "La contaminación del aire causa alrededor de 7 millones de muertes al año.",
    "El 40% de los ríos del mundo están tan contaminados que ya no son aptos para beber.",
    "Cada minuto se tiran al mar más de 1.4 millones de botellas plásticas.",
    "La contaminación del suelo afecta directamente a la agricultura y la salud humana.",
]

# === DATOS SOBRE DEFORESTACIÓN ===
datos_deforestacion = [
    "Cada año se pierden más de 10 millones de hectáreas de bosques.",
    "El 80% de la deforestación está relacionada con la agricultura.",
    "Alrededor del 20% de las emisiones de CO2 provienen de la deforestación.",
    "Se estima que cada segundo se destruye un área de bosque equivalente a una cancha de fútbol.",
    "La deforestación amenaza a más de un millón de especies animales y vegetales.",
]

def get_biodiversidad_image_url():

    return "https://loremflickr.com/800/600/biodiversity,nature,wildlife"

@bot.command('biodiversidad')
async def imagen_biodiversidad(ctx):

    image_url = get_biodiversidad_image_url()
    await ctx.send(image_url)




@bot.event
async def on_ready():
    print(f"Bot conectado como: {bot.user}")

# === COMANDO: PREGUNTA ===
@bot.command()
async def pregunta(ctx):
    """Envía una pregunta aleatoria usando listas separadas."""
    indice = random.randint(0, len(preguntas) - 1)

    bot.indice_pregunta = indice  # Guarda el índice para la respuesta

    await ctx.send(
        f"🌿 **Pregunta:** {preguntas[indice]}\n\n"
        f"(Escribe `$respuesta` para ver la respuesta)"
    )

# === COMANDO: RESPUESTA ===
@bot.command()
async def respuesta(ctx):
    """Muestra la respuesta correspondiente usando el índice guardado."""
    if bot.indice_pregunta is None:
        await ctx.send("Todavía no se ha hecho ninguna pregunta. Usa `$pregunta` primero.")
        return

    await ctx.send(f"✅ **Respuesta:** {respuestas[bot.indice_pregunta]}")

    bot.indice_pregunta = None  # Resetea para evitar repetir respuesta

# === COMANDO INFO ===
@bot.command()
async def info(ctx):
    mensaje = (
        "📚 **Comandos disponibles del bot**\n\n"
        "**$pregunta** → Envía una pregunta aleatoria sobre el medio ambiente.\n"
        "**$respuesta** → Muestra la respuesta de la última pregunta enviada.\n"
        "**$dato** → Muestra un dato curioso sobre la naturaleza y el planeta.\n"
        "**$ecotip** → Envía un consejo ecológico que puedes aplicar en tu vida diaria.\n"
        "**$frase** → Envía una frase inspiradora sobre la naturaleza.\n"
        "**$animal** → Muestra una curiosidad interesante sobre un animal.\n"
        "**$contaminacion** → Envía un dato sobre contaminación ambiental.\n"
        "**$deforestacion** → Muestra información sobre la deforestación en el mundo.\n"
        "**$biodiversidad** → Muestra una imagen de una mariposa.\n\n"
        "🌿 **Usa estos comandos para aprender, inspirarte y cuidar el planeta.**"
    )

    await ctx.send(mensaje)


# === COMANDO DATO ===
@bot.command()
async def dato(ctx):
    await ctx.send(f"📘 **Dato curioso:** {random.choice(datos_curiosos)}")

# === COMANDO ECOTIP ===
@bot.command()
async def ecotip(ctx):
    await ctx.send(f"🌱 **EcoTip:** {random.choice(eco_tips)}")

# === COMANDO FRASE ===
@bot.command()
async def frase(ctx):
    await ctx.send(f"💬 **Frase del día:** {random.choice(frases_inspiradoras)}")

# === COMANDO ANIMAL ===
@bot.command()
async def animal(ctx):
    await ctx.send(f"🐾 **Curiosidad animal:** {random.choice(curiosidades_animales)}")

# === COMANDO CONTAMINACION ===
@bot.command()
async def contaminacion(ctx):
    await ctx.send(f"⚠️ **Dato sobre contaminación:** {random.choice(datos_contaminacion)}")

# === COMANDO DEFORESTACION ===
@bot.command()
async def deforestacion(ctx):
    await ctx.send(f"🌳 **Dato sobre deforestación:** {random.choice(datos_deforestacion)}")


token = ''

bot.run(token)
