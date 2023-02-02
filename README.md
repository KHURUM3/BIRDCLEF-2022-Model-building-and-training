# BIRDCLEF 2022 Model building and training
Redesigned model code for the competition [BirdCLEF 2022](https://www.kaggle.com/competitions/birdclef-2022)

This notebook reveals the capabilities of Pytorch for a simple and efficient construction of a neural network model.

В этом блокноте раскрываются возможности Pytorch для простого и эффективного построения модели нейросети.




## Files of Data

train_metadata.csv - A wide range of metadata is provided for the training data. The most directly relevant fields are:

primary_label - a code for the bird species. You can review detailed information about the bird codes by appending the code to https://ebird.org/species/, such as https://ebird.org/species/amecro for the American Crow.

secondary_labels: Background species as annotated by the recordist. An empty list does not mean that no background birds are audible.

author - the eBird user who provided the recording.

filename: the associated audio file.

rating: Float value between 0.0 and 5.0 as an indicator of the quality rating on Xeno-canto and the number of background species, where 5.0 is the highest and 1.0 is the lowest. 0.0 means that this recording has no user rating yet.

train_audio/ - The bulk of the training data consists of short recordings of individual bird calls generously uploaded by users of xenocanto.org. These files have been downsampled to 32 kHz where applicable to match the test set audio and converted to the ogg format.

test_soundscapes/ - When you submit a notebook, the test_soundscapes directory will be populated with approximately 5,500 recordings to be used for scoring. These are each within a few milliseconds of 1 minute long and in the ogg audio format. Only one soundscape is available for download.

test.csv - Metadata for the test set. Only the first three rows are available for download; the full test.csv is provided in the hidden test set.

    row_id - A unique identifier for the row.
    file_id - A unique identifier for the audio file.
    bird - The ebird code for the row. There is one row for each of the scored species per 5 second window per audio file.
    end_time - The last second of the 5 second time window (5, 10, 15, etc).

sample_submission.csv - A valid sample submission. Only the first three rows are available for download; the full submission.csv is provided in the hidden test set.

    row_id - A unique identifier for the row.
    target - True/False for whether or not the bird in question called during the 5 second window.

scored_birds.json - The subset of the species in the dataset that are scored.

eBird_Taxonomy_v2021.csv - Data on the relationships between different species.


## Данные

train_metadata.csv - для обучающих данных предоставляется широкий спектр метаданных. Наиболее релевантны:

primary_label - код для вида птицы. Вы можете просмотреть подробную информацию о кодах птиц, добавив код к https://ebird.org/species /, такие как https://ebird.org/species/amecro для американской вороны.

secondary_labels: Фоновые виды с комментариями автора записи. Пустой список не означает, что фоновые птицы не слышны.

author: пользователь eBird, предоставивший запись.

filename: соответствующий аудиофайл.

rating: Плавающее значение от 0.0 до 5.0 в качестве показателя оценки качества Xeno-canto и количества фоновых видов, где 5.0 - самый высокий, а 1.0 - самый низкий. 0.0 означает, что у этой записи еще нет рейтинга пользователя.

train_audio/ - Основная часть обучающих данных состоит из коротких записей отдельных птичьих криков, загруженных пользователями xenocanto.org . Эти файлы были уменьшены до 32 кГц, где это применимо, чтобы соответствовать файлам тестового набора, и преобразованы в формат ogg.

test_soundscapes/ - Когда вы отправляете notebook, каталог test_soundscapes будет заполнен примерно 5500 записями, которые будут использоваться для подсчета очков. Каждый из них длится в течение нескольких миллисекунд по 1 минуте и в аудиоформате ogg. Для скачивания доступен только одна звуковая дорожка.

test.csv - метаданные для тестового набора. Для загрузки доступны только первые три строки; полный test.csv предоставляется в скрытом наборе тестов.

    row_id - уникальный идентификатор строки.
    file_id - уникальный идентификатор аудиофайла.
    bird - код ebird для строки. Существует одна строка для каждого из оцененных видов на 5-секундное окно для каждого аудиофайла.
    end_time - последняя секунда 5-секундного временного окна (5, 10, 15 и т.д.).

sample_submission.csv - допустимый образец представления. Для загрузки доступны только первые три строки; полный файл submission.csv предоставляется в скрытом тестовом наборе.

    row_id - уникальный идентификатор для строки.
    target - истина/ложь для определения того, вызывалась ли рассматриваемая птица в течение 5-секундного окна.

scored_birds.json - подмножество видов в наборе данных, которые оцениваются.

eBird_Taxonomy_v2021.csv - данные о взаимоотношениях между различными видами.


