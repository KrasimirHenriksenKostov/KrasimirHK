<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Arbeidsmiljøloven Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .question {
            margin-bottom: 20px;
        }
        .question h2 {
            font-size: 18px;
        }
        .options label {
            display: block;
            margin-bottom: 5px;
        }
        .result {
            font-size: 20px;
            font-weight: bold;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <h1>Arbeidsmiljøloven Quiz</h1>
    <div id="quiz"></div>
    <button onclick="submitQuiz()">Send inn</button>
    <div class="result" id="result"></div>

    <script>
        const quizData = [
            {
                question: "Hva er hovedformålet med arbeidsmiljøloven?",
                options: ["Å regulere lønnsnivåer", "Å sikre et trygt arbeidsmiljø", "Å øke produktiviteten", "Å redusere antall ansatte"],
                correct: 1
            },
            {
                question: "Hvilken paragraf i arbeidsmiljøloven omhandler arbeidsgivers plikt til å sørge for et fullt forsvarlig arbeidsmiljø?",
                options: ["§ 2-1", "§ 3-1", "§ 4-1", "§ 5-1"],
                correct: 2
            },
            {
                question: "Hva er arbeidsgivers plikt ifølge § 3-1 i arbeidsmiljøloven?",
                options: ["Å gi ansatte høyere lønn", "Å sørge for systematisk HMS-arbeid", "Å redusere arbeidstiden", "Å tilby gratis lunsj"],
                correct: 1
            },
            {
                question: "Hva er maksimal tillatt arbeidstid per uke ifølge arbeidsmiljøloven?",
                options: ["35 timer", "37,5 timer", "40 timer", "45 timer"],
                correct: 2
            },
            {
                question: "Hvilken paragraf i arbeidsmiljøloven regulerer overtid?",
                options: ["§ 10-6", "§ 11-1", "§ 12-1", "§ 13-1"],
                correct: 0
            },
            {
                question: "Hva er kravet til pauser ifølge arbeidsmiljøloven § 10-9?",
                options: ["15 minutter hver time", "30 minutter hver 4. time", "30 minutter hver 5. time", "45 minutter hver 6. time"],
                correct: 2
            },
            {
                question: "Hvilken type permisjon er regulert i arbeidsmiljøloven § 12-2?",
                options: ["Svangerskapspermisjon", "Omsorgspermisjon", "Fødselspermisjon", "Foreldrepermisjon"],
                correct: 0
            },
            {
                question: "Hvor mange dager permisjon har en arbeidstaker rett til ved barns sykdom ifølge arbeidsmiljøloven § 12-9?",
                options: ["5 dager", "10 dager", "15 dager", "20 dager"],
                correct: 1
            },
            {
                question: "Hva sier arbeidsmiljøloven § 12-11 om utdanningspermisjon?",
                options: ["Arbeidstaker har rett til permisjon for å ta utdanning som er relevant for stillingen", 
                         "Arbeidstaker har rett til permisjon for å ta hvilken som helst utdanning", 
                         "Arbeidstaker har rett til permisjon for å ta utdanning i utlandet", 
                         "Arbeidstaker har rett til permisjon for å ta utdanning på deltid"],
                correct: 0
            },
            {
                question: "Hva er forbudt ifølge arbeidsmiljøloven § 13-1?",
                options: ["Diskriminering på grunn av politisk syn", 
                          "Diskriminering på grunn av medlemskap i arbeidstakerorganisasjon", 
                          "Diskriminering på grunn av alder", 
                          "Alle de ovennevnte"],
                correct: 3
            },
            {
                question: "Hvilken paragraf i arbeidsmiljøloven omhandler forbud mot diskriminering på grunn av seksuell orientering?",
                options: ["§ 13-1", "§ 13-2", "§ 13-3", "§ 13-4"],
                correct: 0
            },
            {
                question: "Hva sier arbeidsmiljøloven § 13-4 om tilrettelegging for arbeidstakere med nedsatt funksjonsevne?",
                options: ["Arbeidsgiver skal tilrettelegge arbeidet så langt det er mulig", 
                          "Arbeidsgiver skal tilby høyere lønn", 
                          "Arbeidsgiver skal redusere arbeidstiden", 
                          "Arbeidsgiver skal tilby gratis transport"],
                correct: 0
            },
            {
                question: "Hva er kravet til opprettelse av arbeidsmiljøutvalg ifølge arbeidsmiljøloven § 7-1 etter endringen som trådte i kraft 1. januar 2024?",
                options: ["Bedrifter med minst 20 ansatte", 
                          "Bedrifter med minst 30 ansatte", 
                          "Bedrifter med minst 40 ansatte", 
                          "Bedrifter med minst 50 ansatte"],
                correct: 1
            },
            {
                question: "Hvilken paragraf i arbeidsmiljøloven regulerer arbeidsmiljøutvalgets oppgaver?",
                options: ["§ 7-2", "§ 7-3", "§ 7-4", "§ 7-5"],
                correct: 0
            },
            {
                question: "Hva er en av arbeidsmiljøutvalgets hovedoppgaver ifølge arbeidsmiljøloven § 7-2?",
                options: ["Å gi ansatte høyere lønn", 
                          "Å arbeide for et fullt forsvarlig arbeidsmiljø", 
                          "Å redusere arbeidstiden", 
                          "Å tilby gratis lunsj"],
                correct: 1
            },
            {
                question: "Hva er arbeidsgivers plikt ifølge arbeidsmiljøloven § 3-2?",
                options: ["Å sørge for systematisk HMS-arbeid", 
                          "Å gi ansatte høyere lønn", 
                          "Å redusere arbeidstiden", 
                          "Å tilby gratis lunsj"],
                correct: 0
            },
            {
                question: "Hvilken paragraf i arbeidsmiljøloven omhandler arbeidsgivers plikt til å gi opplæring i HMS?",
                options: ["§ 3-5", "§ 3-6", "§ 3-7", "§ 3-8"],
                correct: 0
            },
            {
                question: "Hva sier arbeidsmiljøloven § 3-5 om arbeidsgivers plikt til å gi opplæring i HMS?",
                options: ["Arbeidsgiver skal gi opplæring til alle ansatte", 
                          "Arbeidsgiver skal gi opplæring til ledere og verneombud", 
                          "Arbeidsgiver skal gi opplæring til nyansatte", 
                          "Arbeidsgiver skal gi opplæring til midlertidige ansatte"],
                correct: 1
            },
            {
                question: "Hva defineres som trakassering ifølge arbeidsmiljøloven § 4-3 tredje ledd?",
                options: ["Handlinger som har som formål eller virkning å være krenkende, skremmende, fiendtlige, nedverdigende eller ydmykende", 
                          "Handlinger som har som formål å være morsomme", 
                          "Handlinger som har som formål å være hjelpsomme", 
                          "Handlinger som har som formål å være vennlige"],
                correct: 0
            },
            {
                question: "Hva er arbeidsgivers plikt ved mistanke om trakassering ifølge arbeidsmiljøloven?",
                options: ["Å ignorere problemet", 
                          "Å undersøke og håndtere saken", 
                          "Å gi den mistenkte høyere lønn", 
                          "Å redusere arbeidstiden"],
                correct: 1
            },
            {
                question: "Hva er hovedregelen for ansettelse i staten ifølge statsansatteloven?",
                options: ["Fast ansettelse", 
                          "Midlertidig ansettelse", 
                          "Ansettelse på prøve", 
                          "Ansettelse på deltid"],
                correct: 0
            },
            {
                question: "Hva er maksimal varighet for midlertidig ansettelse før arbeidstaker har krav på fast ansettelse ifølge statsansatteloven?",
                options: ["1 år", "2 år", "3 år", "4 år"],
                correct: 2
            },
            {
                question: "Hva er arbeidsgivers plikt ved utløp av en midlertidig ansettelse ifølge arbeidsmiljøloven?",
                options: ["Å tilby fast ansettelse", 
                          "Å gi skriftlig varsel om opphør", 
                          "Å gi høyere lønn", 
                          "Å redusere arbeidstiden"],
                correct: 1
            },
            {
                question: "Hva skal en arbeidsavtale minst omfatte ifølge arbeidsmiljøloven § 14-6?",
                options: ["Lønn og arbeidstid", 
                          "Arbeidsoppgaver og arbeidssted", 
                          "Varighet av arbeidsforholdet", 
                          "Alle de ovennevnte"],
                correct: 3
            },
            {
                question: "Når skal en skriftlig arbeidsavtale foreligge ifølge arbeidsmiljøloven § 14-5?",
                options: ["Snarest mulig og senest én måned etter at arbeidsforholdet begynte", 
                          "Snarest mulig og senest tre måneder etter at arbeidsforholdet begynte", 
                          "Snarest mulig og senest seks måneder etter at arbeidsforholdet begynte", 
                          "Snarest mulig og senest ett år etter at arbeidsforholdet begynte"],
                correct: 0
            },
            {
                question: "Hva er en arbeidstakers reservasjonsrett ved virksomhetsoverdragelse ifølge arbeidsmiljøloven § 16-3?",
                options: ["Retten til å motsette seg at arbeidsforholdet overføres til ny arbeidsgiver", 
                          "Retten til å kreve høyere lønn", 
                          "Retten til å redusere arbeidstiden", 
                          "Retten til å få gratis lunsj"],
                correct: 0
            },
            {
                question: "Hva er fristen for å utøve reservasjonsretten ved virksomhetsoverdragelse ifølge arbeidsmiljøloven § 16-3?",
                options: ["7 dager", "14 dager", "21 dager", "30 dager"],
                correct: 1
            },
            {
                question: "Hva er arbeidsgivers plikt ved virksomhetsoverdragelse ifølge arbeidsmiljøloven § 16-2?",
                options: ["Å informere arbeidstakerne om overdragelsen", 
                          "Å gi arbeidstakerne høyere lønn", 
                          "Å redusere arbeidstakernes arbeidstid", 
                          "Å tilby gratis lunsj"],
                correct: 0
            },
            {
                question: "Hva er definisjonen av utleie av arbeidstakere ifølge arbeidsmarkedsloven?",
                options: ["Leie av arbeidstakere fra en arbeidsgiver til en oppdragsgiver der de innleide er underlagt oppdragsgivers ledelse", 
                          "Leie av arbeidstakere fra en arbeidsgiver til en oppdragsgiver der de innleide er underlagt arbeidsgivers ledelse", 
                          "Leie av arbeidstakere fra en oppdragsgiver til en arbeidsgiver der de innleide er underlagt oppdragsgivers ledelse", 
                          "Leie av arbeidstakere fra en oppdragsgiver til en arbeidsgiver der de innleide er underlagt arbeidsgivers ledelse"],
                correct: 0
            },
            {
                question: "Hva er hovedregelen for innleie av arbeidstakere ifølge statsansatteloven?",
                options: ["Innleie er tillatt for en begrenset periode", 
                          "Innleie er tillatt for en ubegrenset periode", 
                          "Innleie er ikke tillatt", 
                          "Innleie er tillatt uten restriksjoner"],
                correct: 0
            },
            {
                question: "Hva er vikarbyrådirektivets prinsipp om likebehandling ved utleie fra bemanningsforetak?",
                options: ["Utleid arbeidstaker skal minst sikres de vilkår som ville kommet til anvendelse dersom arbeidstaker hadde vært ansatt hos innleier for å utføre samme arbeid", 
                          "Utleid arbeidstaker skal sikres høyere lønn enn innleiers ansatte", 
                          "Utleid arbeidstaker skal sikres kortere arbeidstid enn innleiers ansatte", 
                          "Utleid arbeidstaker skal sikres lengre pauser enn innleiers ansatte"],
                correct: 0
            }
        ];

        const quizContainer = document.getElementById('quiz');

        function loadQuiz() {
            quizData.forEach((quizItem, index) => {
                const quizDiv = document.createElement('div');
                quizDiv.className = 'question';
                const questionTitle = document.createElement('h2');
                questionTitle.textContent = quizItem.question;
                quizDiv.appendChild(questionTitle);
                
                const optionsDiv = document.createElement('div');
                optionsDiv.className = 'options';
                quizItem.options.forEach((option, i) => {
                    const label = document.createElement('label');
                    const input = document.createElement('input');
                    input.type = 'radio';
                    input.name = `question${index}`;
                    input.value = i;
                    label.appendChild(input);
                    label.appendChild(document.createTextNode(option));
                    optionsDiv.appendChild(label);
                });
                quizDiv.appendChild(optionsDiv);
                quizContainer.appendChild(quizDiv);
            });
        }

        function submitQuiz() {
            let score = 0;
            quizData.forEach((quizItem, index) => {
                const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
                if (selectedOption && parseInt(selectedOption.value) === quizItem.correct) {
                    score++;
                }
            });
            const resultDiv = document.getElementById('result');
            resultDiv.textContent = `Din endelige poengsum er: ${score} av ${quizData.length}`;
        }

        loadQuiz();
    </script>
</body>
</html>
