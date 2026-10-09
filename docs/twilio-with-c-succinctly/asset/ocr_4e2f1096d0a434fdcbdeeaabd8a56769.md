```
string val = Request.Query["Digits"].Value;
if (val != null && val != string.Empty)
{
    using (SimpleAnsweringMachine sam = new SimpleAnsweringMachine())
    {
        if (userId == string.Empty)
        {
            if (val.Length > 1)
            {
                userId = val;

                if (questions == null)
                    questions = sam.GetQuestions();

                res = ProcessQuestion(sam, string.Empty);
            }
            else
                res = "<Response><Say voice=\"woman\">No valid option entered.</Say></Response>";
        }
        else
        {
            string[] pa =
                sam.GetPredefinedAnswers(currentQuestion.ToString());

            foreach (string p in pa)
            {
                string[] parts = p.Split('|');

                if (parts[0].ToLower().Contains(val.ToLower()))
                {
                    sam.InsertSurveyResponse("q" +
                        currentQuestion.ToString(), userId, parts[0]);

                    string nxtQ =
                        (currentQuestion < questions.Length) ?
                        "<Say voice=\"woman\">Please hold for the next question...</Say>" :
                        "<Say voice=\"woman\">The survey is complete. Thank you.</Say>";

                    if (currentQuestion < questions.Length)
                    {
                        res = "<Say voice=\"woman\">Answer... " +
                            parts[0][1] + " saved for question... " +
                            currentQuestion.ToString() + "</Say>" +
                            nxtQ;
```
```