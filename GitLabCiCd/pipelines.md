[⇐ readme](../readme.md)

## pipelines

---

Это то, что вы определяете в `.gitlab-ci.yml` и то,
<br> что происходит, когда содержимое файла запускается ранером.

Пайплайны формируют задачи и этапы.

Этапы формируют порядок выполнения. 
<br>Типичные этапы это: `build`, `test` и `deploy`.

Задачи определяют специфичные задачи внутри каждого этапа.
Для примера, джоба может компилировать или тестировать код.

Пайплайны могут реагировать на разные события, 
<br>такие как коммиты или мерджи, или в отложенном режиме.

Внутри пайплана вы можете интегрироваться 
<br>с большим диапазоном инструментов и платформ.

