# Sentimental-analysis
{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyPqMw6s5H0BccJCPoevy4Zq"
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "code",
      "source": [
        "import nltk\n",
        "nltk.download('punkt_tab')"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "CZw4U3rmt-t7",
        "outputId": "9d66a799-b58d-40fa-8bde-1f34362c702c"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "[nltk_data] Downloading package punkt_tab to /root/nltk_data...\n",
            "[nltk_data]   Unzipping tokenizers/punkt_tab.zip.\n"
          ]
        },
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "True"
            ]
          },
          "metadata": {},
          "execution_count": 5
        }
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "bC4_DLv-s7em",
        "outputId": "2c50f1d3-fa1f-42a4-86a1-b43f7f4bdcd1"
      },
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Name : Priya Behera\n",
            "PRN : 20230804022\n",
            "Name : Priya Behera \n",
            "PRN : 20230804022\n"
          ]
        },
        {
          "output_type": "stream",
          "name": "stderr",
          "text": [
            "[nltk_data] Downloading package vader_lexicon to /root/nltk_data...\n",
            "[nltk_data]   Package vader_lexicon is already up-to-date!\n",
            "[nltk_data] Downloading package punkt to /root/nltk_data...\n",
            "[nltk_data]   Package punkt is already up-to-date!\n",
            "[nltk_data] Downloading package stopwords to /root/nltk_data...\n",
            "[nltk_data]   Package stopwords is already up-to-date!\n",
            "[nltk_data] Downloading package wordnet to /root/nltk_data...\n",
            "[nltk_data]   Package wordnet is already up-to-date!\n"
          ]
        },
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "True"
            ]
          },
          "metadata": {},
          "execution_count": 6
        }
      ],
      "source": [
        "#1\n",
        "print(\"Name : Priya Behera\\nPRN : 20230804022\")\n",
        "import nltk\n",
        "nltk.download('vader_lexicon')\n",
        "#2\n",
        "print(\"Name : Priya Behera \\nPRN : 20230804022\")\n",
        "import nltk\n",
        "from nltk.tokenize import word_tokenize\n",
        "from nltk.corpus import stopwords\n",
        "from nltk.stem import WordNetLemmatizer\n",
        "from textblob import TextBlob\n",
        "\n",
        "nltk.download('punkt')\n",
        "nltk.download('stopwords')\n",
        "nltk.download('wordnet')\n",
        "\n",
        "\n"
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# Example text data\n",
        "text_data = [\n",
        "    \"I absolutely love this product, it has transformed my life!\",\n",
        "    \"The new design is okay, but I expected something more innovative.\",\n",
        "    \"I had a horrible experience with the customer service.\",\n",
        "    \"This brand really understands what customers want. Highly recommended!\",\n",
        "    \"The product is decent but nothing special.\",\n",
        "    \"I'm never buying from this company again, totally disappointed.\"\n",
        "]\n",
        "print(text_data)\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "DVjcqFNztae1",
        "outputId": "5aa6e22c-486c-4f7d-e1cd-6462ca8ab60c"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "['I absolutely love this product, it has transformed my life!', 'The new design is okay, but I expected something more innovative.', 'I had a horrible experience with the customer service.', 'This brand really understands what customers want. Highly recommended!', 'The product is decent but nothing special.', \"I'm never buying from this company again, totally disappointed.\"]\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# Preprocessing\n",
        "lemmatizer = WordNetLemmatizer()\n",
        "stop_words = set(stopwords.words('english'))\n",
        "\n",
        "def preprocess(text):\n",
        "    tokens = word_tokenize(text.lower())\n",
        "    # Remove stopwords and apply lemmatization\n",
        "    processed_tokens = [lemmatizer.lemmatize(word) for word in tokens if word not in stop_words and word.isalnum()]\n",
        "    return processed_tokens\n",
        "\n"
      ],
      "metadata": {
        "id": "Oj2abnZrtnMB"
      },
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "source": [
        "# Apply preprocessing to the dataset\n",
        "processed_data = [preprocess(sentence) for sentence in text_data]\n",
        "print(processed_data)\n",
        "\n",
        "# Perform sentiment analysis using TextBlob\n",
        "def analyze_sentiment(text):\n",
        "    blob = TextBlob(text)\n",
        "    return blob.sentiment.polarity\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "RFqixGIutrji",
        "outputId": "9e34ce81-6ad0-4fd3-ea19-6807b2a9a3a7"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "[['absolutely', 'love', 'product', 'transformed', 'life'], ['new', 'design', 'okay', 'expected', 'something', 'innovative'], ['horrible', 'experience', 'customer', 'service'], ['brand', 'really', 'understands', 'customer', 'want', 'highly', 'recommended'], ['product', 'decent', 'nothing', 'special'], ['never', 'buying', 'company', 'totally', 'disappointed']]\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "# Define custom sentiment classification function\n",
        "def classify_sentiment(score):\n",
        "    if score > 0.3:\n",
        "        return \"Positive\"\n",
        "    elif score < -0.2:\n",
        "        return \"Negative\"\n",
        "    else:\n",
        "        return \"Neutral\"\n",
        "\n",
        "# Analyze sentiment\n",
        "sentiment_scores = [analyze_sentiment(sentence) for sentence in text_data]\n",
        "\n",
        "# results\n",
        "for sentence, score in zip(text_data, sentiment_scores):\n",
        "    sentiment = classify_sentiment(score)\n",
        "    print(f\"Text: {sentence}\\nSentiment: {sentiment} (Score: {score})\\n\")\n",
        "\n"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "Jq_-klqbtwCX",
        "outputId": "a81115a3-a6b1-464b-f559-343cecb279fc"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Text: I absolutely love this product, it has transformed my life!\n",
            "Sentiment: Positive (Score: 0.625)\n",
            "\n",
            "Text: The new design is okay, but I expected something more innovative.\n",
            "Sentiment: Positive (Score: 0.30727272727272725)\n",
            "\n",
            "Text: I had a horrible experience with the customer service.\n",
            "Sentiment: Negative (Score: -1.0)\n",
            "\n",
            "Text: This brand really understands what customers want. Highly recommended!\n",
            "Sentiment: Neutral (Score: 0.2)\n",
            "\n",
            "Text: The product is decent but nothing special.\n",
            "Sentiment: Neutral (Score: 0.2619047619047619)\n",
            "\n",
            "Text: I'm never buying from this company again, totally disappointed.\n",
            "Sentiment: Negative (Score: -0.75)\n",
            "\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [
        "\n",
        "# Classify sentiment based on polarity score\n",
        "def classify_sentiment(score):\n",
        "    if score > 0:\n",
        "        return \"Positive\"\n",
        "    elif score < 0:\n",
        "        return \"Negative\"\n",
        "    else:\n",
        "        return \"Neutral\"\n",
        "\n",
        "# Convert polarity to percentage\n",
        "def polarity_to_percentage(score):\n",
        "    return (score + 1) * 50  # Converts -1 to +1 range into 0 to 100%\n",
        "# Analyze and display results with percentage\n",
        "sentiment_scores = [analyze_sentiment(sentence) for sentence in text_data]\n",
        "sentiments = [classify_sentiment(score) for score in sentiment_scores]\n",
        "# Calculate overall percentages\n",
        "total_count = len(sentiments)\n",
        "positive_count = sentiments.count(\"Positive\")\n",
        "negative_count = sentiments.count(\"Negative\")\n",
        "neutral_count = sentiments.count(\"Neutral\")\n",
        "\n",
        "positive_percentage = (positive_count / total_count) * 100\n",
        "negative_percentage = (negative_count / total_count) * 100\n",
        "neutral_percentage = (neutral_count / total_count) * 100\n",
        "# Print results\n",
        "print(\"Overall Sentiment Analysis:\")\n",
        "print(f\"Positive Sentiment: {positive_percentage:.2f}%\")\n",
        "print(f\"Negative Sentiment: {negative_percentage:.2f}%\")\n",
        "print(f\"Neutral Sentiment: {neutral_percentage:.2f}%\")"
      ],
      "metadata": {
        "colab": {
          "base_uri": "https://localhost:8080/"
        },
        "id": "NGmFA8Jsui_m",
        "outputId": "96eb65eb-13ee-4d0e-84cd-8158be7e7d14"
      },
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "name": "stdout",
          "text": [
            "Overall Sentiment Analysis:\n",
            "Positive Sentiment: 66.67%\n",
            "Negative Sentiment: 33.33%\n",
            "Neutral Sentiment: 0.00%\n"
          ]
        }
      ]
    },
    {
      "cell_type": "code",
      "source": [],
      "metadata": {
        "id": "zFRmUhMnumDu"
      },
      "execution_count": null,
      "outputs": []
    }
  ]
}
