<script>
    //* Подгружаю контент окна предыстории
window.addEventListener('load', () => {
    //* Скрываю заставку и отображаю контент
    // Убираю заставку
    setTimeout(() => {
        document.querySelector('.backstory-popup__title-screen').classList.add('backstory-popup__title-screen--transparent');
    }, 3500);
    setTimeout(() => {
        document.querySelector('.backstory-popup__title-screen').classList.add('backstory-popup__title-screen--inactive');
    }, 5000);
    // Показываю контент
    setTimeout(() => {
        document.querySelector('.backstory-popup__content').classList.add('backstory-popup__content--active');
        // Cлайды
        const slides = Array.from(document.querySelectorAll('.backstory-popup__slide'));
        slides[0].classList.add('backstory-popup__slide--active'); // Заранее активирую первый слайд
        
        // Кнопки, ведущие на следующий слайд
        const slideBtnsBlue = Array.from(document.querySelectorAll('.backstory-popup__btn--blue'));
        const slideBtnsOrange = Array.from(document.querySelectorAll('.backstory-popup__btn--orange'));

        // Для анимации видеозаписи, вызова палиции и эффекта фотосъёмки
        const photographingBtn = [
            slideBtnsOrange[1],
            slideBtnsOrange[4]
        ];
        const photographingScreen = Array.from(document.querySelectorAll('.backstory-popup__slide-photographing-screen'));
        const recordingBtn = slideBtnsOrange[3]; // Кнопка для активации эффекта видеозаписи
        const recordingScreen = document.querySelector('.backstory-popup__slide-recording-screen');
        const policeCallingBtn = slideBtnsOrange[2];
        const policeCallingScreen = document.querySelector('.backstory-popup__slide-police-calling-screen');
        
        // Содержимое слайдо
        const bubble = Array.from(document.querySelectorAll('.backstory-popup__bubble'));
        const narrator = Array.from(document.querySelectorAll('.backstory-popup__narrator'));
        
        // Строки, которым нужно добавить эффект печатной машинки
        const slide1Strings1s = Array.from(document.querySelectorAll('.backstory-popup__slide-1 .backstory-popup__typing-string--1s'));
        const slide1Strings2s = Array.from(document.querySelectorAll('.backstory-popup__slide-1 .backstory-popup__typing-string--2s'));
        
        const slide2Strings2s = Array.from(document.querySelectorAll('.backstory-popup__slide-2 .backstory-popup__typing-string--2s'));
        
        const slide3Strings1s = Array.from(document.querySelectorAll('.backstory-popup__slide-3 .backstory-popup__typing-string--1s'));
        
        const slide4Strings1s = Array.from(document.querySelectorAll('.backstory-popup__slide-4 .backstory-popup__typing-string--1s'));
        const slide4Strings2s = Array.from(document.querySelectorAll('.backstory-popup__slide-4 .backstory-popup__typing-string--2s'));
        
        const slide5Strings2s = Array.from(document.querySelectorAll('.backstory-popup__slide-5 .backstory-popup__typing-string--2s'));
        const slide5Strings1s = Array.from(document.querySelectorAll('.backstory-popup__slide-5 .backstory-popup__typing-string--1s'));
        
        const slide6Strings1s = Array.from(document.querySelectorAll('.backstory-popup__slide-6 .backstory-popup__typing-string--1s'));
        const slide6Strings2s = Array.from(document.querySelectorAll('.backstory-popup__slide-6 .backstory-popup__typing-string--2s'));
        
        // Вторая половина прямоугольника рассказчика
        const narratorRow2 = Array.from(document.querySelectorAll('.backstory-popup__narrator-row-2'));
        
        // Кнопка перезапуска слайдера окна 
        const restartBtn = document.querySelector('.backstory-popup__btn-restart');


        // * Функция поочерёдного отображения содержимого слайда окна
        function addBackstoryPopupSlideContent(
            functionDelay, // Задержка перед началом выполнения функции
            // * Для строк
            typingStringsElements, // Строки
            stringDelays, // Задержки печатания строк
            // * Для содержимого слайдов
            activeBubble, // Активный пузырь реплики
            activeNarrator, // Активный прямоугольник рассказчика
            activeNarratorDelay, // Задержка перед отображением прямоугольника рассказчика
            // * Вторая половина прямоугольника рассказчика
            activeNarratorRow2, // Элемент с кнопками и формами
            activeNarratorRow2Delay, // Задержка перед отображением элемента с кнопками и формами
            // * Флаги отслеживания
            isPopupHasBubble // Флаг для отслеживания наличия пузыря реплики
        ) {
            // Задержка перед началом выполнения функции
            setTimeout(() => {
                // Задаю активный класс пузырю реплики взависимости от значения аргументв
                if (activeBubble === bubble[0]) {
                    activeBubble.classList.add('backstory-popup__bubble-1--active')
                } else if (activeBubble === bubble[1]) {
                    activeBubble.classList.add('backstory-popup__bubble-2--active')
                } else if (activeBubble === bubble[3]) {
                    activeBubble.classList.add('backstory-popup__bubble-4--active')
                };
        
                // Задаю активный класс строкам поочередно
                let delay = 0;
                for (let i = 0; i < typingStringsElements.length; i++) {
                    setTimeout(() => {
                        // Если пузыря нет, добавляю задержку строкам прямоугольника рассказчика
                        if (!isPopupHasBubble) {
                            setTimeout(() => {
                                // Добавляю активный класс текущей строке
                                typingStringsElements[i].classList.add('backstory-popup__typing-string--active');
                            }, 1000);
                        } else {
                            // Добавляю активный класс текущей строке
                            typingStringsElements[i].classList.add('backstory-popup__typing-string--active');
                        }
        
                        // После завершения печати всех строк, добавляю активный класс "activeNarrator"
                        setTimeout(() => {
                            activeNarrator.classList.add('backstory-popup__narrator--active');
                        }, activeNarratorDelay);
        
                        // Если это последняя строка, добавляю активный класс "activeNarratorRow2"
                        if (i === typingStringsElements.length - 1) {
                            setTimeout(() => {
                                activeNarratorRow2.classList.add('backstory-popup__narrator-row-2--active');
                            }, activeNarratorRow2Delay);
                        }
                    }, delay);
                    // Увеличиваю задержку перед добавлением следующего активного класса
                    delay += stringDelays[i];
                }
            }, functionDelay);
        };


        // * Функция плавного переключения слайдов
        function smoothSlideChanging(slideNames) {
            slideNames[0].classList.add('backstory-popup__slide--transparent');
            setTimeout(() => {
                slideNames[0].classList.remove('backstory-popup__slide--active');
            }, 1000)
            setTimeout(() => {
                slideNames[1].classList.add('backstory-popup__slide--active');
            }, 2000)
        };


        // * Функция сияния кнопки
        function shiningBtnAnimation() {
            slideBtnsBlue[0].classList.toggle('backstory-popup__btn--blue-shining'); // Добавляем/удаляем класс анимации
            setTimeout(shiningBtnAnimation, 2000); // Запускаем функцию снова через 2 секунды
        };


        // * Функция переключения слайдов по клику
        function nextSlide(btnName, slideNames) {
            btnName.addEventListener('click', (event) => {
                // Взависимости от 2-го значания slideNames применять соответствующий скрипт

                // * Для 2-го слайда
                if (slideNames[1] === slides[1]) {
                    smoothSlideChanging(slideNames);
                    addBackstoryPopupSlideContent(
                        2500,
                        [slide2Strings2s[0], slide2Strings2s[1]], // Строки рассказчика
                        [1800, 1800],
                        null, // Убрал активацию пузыря реплики
                        narrator[1],
                        0,
                        narratorRow2[1],
                        3000,
                        false
                    );
                }


                // * Для 3-го слайда
                else if (slideNames[1] === slides[2]) {
                    // Локальная функция (чтобы не дублировать код)
                    function localFunction1(slideNames) {
                        smoothSlideChanging(slideNames);
                        addBackstoryPopupSlideContent(
                            4000,
                            [slide3Strings1s[0], slide3Strings1s[1], slide3Strings1s[2]], // Строки пузыря реплики
                            [1000, 1000, 1000],
                            bubble[0],
                            narrator[2],
                            2800,
                            narratorRow2[2],
                            1000,
                            true
                        );
                    }
                    // С эффектом фотосъёмки
                    if (btnName === photographingBtn[0]) {
                        narrator[1].classList.add('backstory-popup__element--transparent');
                        photographingScreen[0].classList.add('backstory-popup__slide-photographing-screen--active');
                        setTimeout(() => {
                            narrator[1].classList.remove('backstory-popup__narrator--active');
                        }, 1000);
                        setTimeout(() => {
                            localFunction1(slideNames) 
                        }, 2500);
                    } 
                    // С анимацией вызова полиции
                    else if (btnName === policeCallingBtn) {
                        narrator[1].classList.add('backstory-popup__element--transparent');
                        policeCallingScreen.classList.add('backstory-popup__slide-police-calling-screen--active');
                        setTimeout(() => {
                            narrator[1].classList.remove('backstory-popup__narrator--active');
                        }, 1000);
                        setTimeout(() => {
                            localFunction1(slideNames) 
                        }, 2500);
                    } 
                    // По умолчанию
                    else {
                        localFunction1(slideNames);
                    }
                }


                // * Для 4-го слайда
                else if (slideNames[1] === slides[3]) {
                    // Локальная функция (чтобы не дублировать код)
                    function localFunction2(slideNames) {
                        smoothSlideChanging(slideNames);
                        addBackstoryPopupSlideContent(
                            3000,
                            [
                                slide4Strings1s[0], slide4Strings1s[1], slide4Strings1s[2], slide4Strings1s[3], // Строки пузыря реплики
                                slide4Strings2s[0], // Строки рассказчика
                            ],
                            [1000, 1000, 1000, 1000, 1800, 1000, 1000, 1000],
                            bubble[1],
                            narrator[3],
                            1800,
                            narratorRow2[3],
                            1800,
                            true
                        );
                    }
                    // С анимацией видеозаписи
                    if (btnName === recordingBtn) {
                        bubble[0].classList.add('backstory-popup__element--transparent');
                        narrator[2].classList.add('backstory-popup__element--transparent');
                        recordingScreen.classList.add('backstory-popup__slide-recording-screen--active');
                        setTimeout(() => {
                            bubble[0].classList.remove('backstory-popup__bubble-1--active');
                            narrator[2].classList.remove('backstory-popup__narrator--active');
                        }, 1000);
                        setTimeout(() => {
                            localFunction2(slideNames) 
                        }, 4000);
                    } 
                    // С эффектом фотосъёмки
                    else if (btnName === photographingBtn[1]) {
                        bubble[0].classList.add('backstory-popup__element--transparent');
                        narrator[2].classList.add('backstory-popup__element--transparent');
                        photographingScreen[1].classList.add('backstory-popup__slide-photographing-screen--active');
                        setTimeout(() => {
                            bubble[0].classList.remove('backstory-popup__bubble-1--active');
                            narrator[2].classList.remove('backstory-popup__narrator--active');
                        }, 1000);
                        setTimeout(() => {
                            localFunction2(slideNames) 
                        }, 2500);
                    } 
                    // По умолчанию
                    else {
                        localFunction2(slideNames);
                    }
                }


                // * Для 5-го слайда
                else if (slideNames[1] === slides[4]) {
                    event.preventDefault();
                    bubble[1].classList.add('backstory-popup__element--transparent');
                    narrator[3].classList.add('backstory-popup__element--transparent');
                    setTimeout(() => {
                        bubble[1].classList.remove('backstory-popup__bubble-2--active');
                        narrator[3].classList.remove('backstory-popup__narrator--active');
                    }, 1000);
                    
                    // Активирую второй пузырь реплики на слайде и его текст
                    bubble[2].classList.add('backstory-popup__bubble-3--active');
                    slide4Strings1s[4].classList.add('backstory-popup__typing-string--active');
                    setTimeout(() => {
                        slide4Strings1s[5].classList.add('backstory-popup__typing-string--active');
                    }, 1800);
                    setTimeout(() => {
                        slide4Strings1s[6].classList.add('backstory-popup__typing-string--active');
                    }, 3600);

                    // Задержка перед вызовом функции для 5-го слайда
                    setTimeout(() => {
                        smoothSlideChanging(slideNames);
                        addBackstoryPopupSlideContent(
                            3500,
                            [slide5Strings2s[0], slide5Strings1s[0]], // Строки рассказчика
                            [1800, 1000],
                            null, // Убрал активацию пузыря реплики
                            narrator[4],
                            1000,
                            narratorRow2[4],
                            2800,
                            false
                        );
                    }, 5000); 
                }


                // * Для 6-го слайда
                else if (slideNames[1] === slides[5]) {
                    event.preventDefault();
                    smoothSlideChanging(slideNames);
                    addBackstoryPopupSlideContent(
                        3000,
                        [
                            slide6Strings1s[0], slide6Strings1s[1], slide6Strings1s[2], // Строки пузыря реплики
                            slide6Strings2s[0], slide6Strings2s[1], slide6Strings1s[3] // Строки рассказчика
                        ], // Строки рассказчика
                        [1000, 1000, 1000, 1800, 1800, 1000],
                        bubble[3],
                        narrator[5],
                        1800,
                        narratorRow2[5],
                        1800,
                        true
                    );
                    // Активирую кнопку перезапуска слайдера окна
                    setTimeout(() => {
                        restartBtn.classList.add('backstory-popup__btn-restart--active');
                    }, 13000);
                };
            });
        };

        // * Вызов функции переключения слайдов по клику
        // Для 1-го слайда
        addBackstoryPopupSlideContent(
            500,
            [slide1Strings1s[0], slide1Strings2s[0]], // Строки рассказчика
            [1000, 4000],
            null, // Убрал активацию пузыря реплики
            narrator[0],
            0,
            narratorRow2[0],
            3500,
            false
        );
        setTimeout(shiningBtnAnimation, 7500); // Запускаю сияние через 3c после появления 1-го слайда

        // Для 2-го слайда
        nextSlide(slideBtnsBlue[0], [slides[0], slides[1]]);
        // Для 3-го слайда
        nextSlide(slideBtnsOrange[0], [slides[1], slides[2]]);
        nextSlide(photographingBtn[0], [slides[1], slides[2]]); // С эффектом фотосъёмки
        nextSlide(policeCallingBtn, [slides[1], slides[2]]); // С анимацией вызова полиции
        // Для 4-го слайда
        nextSlide(recordingBtn, [slides[2], slides[3]]); // С анимацией видеозаписи
        nextSlide(photographingBtn[1], [slides[2], slides[3]]); // С эффектом фотосъёмки
        nextSlide(slideBtnsOrange[5], [slides[2], slides[3]]);
        // Для 5-го слайда
        nextSlide(slideBtnsBlue[1], [slides[3], slides[4]]);
        //  Для 6-го слайда
        nextSlide(slideBtnsOrange[6], [slides[4], slides[5]]);
    }, 6000);
});
</script>