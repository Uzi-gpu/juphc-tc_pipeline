# Cloud IDE steps (Parts B and C)

Open this lab in your Coursera account (you must be logged in):

https://labs.cognitiveclass.ai/v2/tools/cloud-ide-openshift?ulid=ulid-62a5d7a1c4cf2192fb40ae2fc139b27b9966d688

The Cloud IDE already contains `tax_calculator` and `tc-pipeline`. If `tax_calculator` is missing, clone it:

```bash
cd /home/project
git clone https://github.com/ibm-developer-skills-network/zntwk-tax_calculator.git tax_calculator
cd tax_calculator
```

Copy the files from this folder into the matching Cloud IDE folders if the lab starter is older.

---

## Screenshot 01 — Jasmine tests (1 point)

```bash
cd /home/project/tax_calculator
npm install
npx jasmine
```

You need: `7 specs, 0 failures`

---

## Screenshot 02 — Dockerfile (1 point)

Open `tax_calculator/Dockerfile`. It must start with `FROM nginx` and copy these five files:

```
FROM nginx
COPY favicon.ico /usr/share/nginx/html/favicon.ico
COPY index.html /usr/share/nginx/html/index.html
COPY script.js /usr/share/nginx/html/script.js
COPY style.css /usr/share/nginx/html/style.css
COPY taxCalculator.js /usr/share/nginx/html/taxCalculator.js
```

---

## Screenshot 03 — Build the image (1 point)

```bash
cd /home/project/tax_calculator
docker build -t tax-calculator .
docker images
```

---

## Screenshot 04 — Run locally on port 8080 (1 point)

```bash
docker run -d --name tax-calculator -p 8080:80 tax-calculator
```

Open the app in the Cloud IDE browser / preview on port 8080. Capture the Tax Calculator page.

---

## Screenshot 05 — Tag and push to IBM Cloud Registry (1 point)

```bash
docker tag tax-calculator us.icr.io/${SN_ICR_NAMESPACE}/tax-calculator
docker push us.icr.io/${SN_ICR_NAMESPACE}/tax-calculator
```

---

## Screenshot 06 — Deploy on IBM Cloud Code Engine (1 point)

Use the lab’s Code Engine commands (usually already logged in). Typical commands:

```bash
ibmcloud ce app create --name tax-calculator \
  --image us.icr.io/${SN_ICR_NAMESPACE}/tax-calculator \
  --registry-secret icr-secret \
  --port 80
ibmcloud ce app get --name tax-calculator
```

If `create` says the app already exists:

```bash
ibmcloud ce app update --name tax-calculator \
  --image us.icr.io/${SN_ICR_NAMESPACE}/tax-calculator
```

Open the Code Engine URL and screenshot the running app.

---

## Screenshot 07 — Tekton tasks (1 point)

In Cloud IDE, open `tc-pipeline/tasks.yaml` and add the `npm` and `jasmine` tasks from this repo’s `tc-pipeline/tasks.yaml`.

Then apply:

```bash
cd /home/project/tc-pipeline
kubectl apply -f tasks.yaml
```

---

## Screenshot 08 — Extend the pipeline (1 point)

In `tc-pipeline/pipeline.yaml`, insert `npminstall` and `tests` after `clone`, and make `build` run after `tests`. Use this repo’s `pipeline.yaml` as the finished file.

```bash
kubectl apply -f pipeline.yaml
kubectl apply -f pvc.yaml
```

---

## Screenshot 09 — PipelineRun (1 point)

1. Push `tax_calculator` to your GitHub (create repo `tax_calculator` if needed).
2. Change the heading in `index.html` to **Tax Calculator V2** and push a `v2` branch.
3. In `run.yaml`, set `repo-url` to your GitHub URL and `branch: "v2"`.

```bash
kubectl apply -f run.yaml
tkn pipelinerun logs -f --last
```

---

## Screenshot 10 — Deployed pipeline image (1 point)

After the pipeline succeeds, open the Code Engine URL. The page should show **Tax Calculator V2**.

---

## Submission

Use **Option 1: AI-Graded Submission** and upload the 10 screenshots plus any URLs the form asks for.
