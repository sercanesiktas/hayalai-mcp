# hayalai-mcp

[HayalAI](https://github.com/sercanesiktas/hayalai) prompt kütüphanesi için bir MCP sunucusu. Claude Code, Claude Desktop ve Cursor gibi istemciler, Türkçe açıklamalı 17 binden fazla prompt içinde arama yapıp seçtikleri promptun metnini alabilir.

## Araçlar

| Araç | Açıklama |
|---|---|
| `prompt_ara` | Başlık ve Türkçe açıklamada arar. `kategori` ve `arac` ile daraltılabilir, `adet` ile sınırlanır. |
| `prompt_getir` | Başlığı verilen promptun tam metnini döner. Uzun promptlar `maks_karakter` ile kesilebilir. |
| `rastgele_prompt` | Verilen kategori ve araca uyan rastgele bir promptu tam metniyle döner. |
| `kategoriler` | Kategori ve araç bazında prompt sayıları. |

Aramada Türkçe karakterler eşitlenir, `iyilestirme` sorgusu `İyileştirme` ile de eşleşir. Birden fazla kelime verilirse hepsi başlıkta ya da açıklamada geçmelidir.

## Kurulum

Node.js 18 veya üzeri gerekir.

```bash
git clone https://github.com/sercanesiktas/hayalai-mcp.git
cd hayalai-mcp
npm install
```

İlk çalıştırmada sunucu [`prompts.csv`](https://github.com/sercanesiktas/hayalai/blob/main/prompts.csv) dosyasını (yaklaşık 31 MB) indirip `~/.cache/hayalai-mcp/` altında saklar. Kopya 7 günden eskiyse yeniden indirilir, bağlantı yoksa eski kopya kullanılır.

## İstemci ayarları

Claude Code:

```bash
claude mcp add hayalai -- node /tam/yol/hayalai-mcp/sunucu.js
```

Claude Desktop (`claude_desktop_config.json`) ve Cursor (`~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "hayalai": {
      "command": "node",
      "args": ["/tam/yol/hayalai-mcp/sunucu.js"]
    }
  }
}
```

## Yapılandırma

| Ortam değişkeni | Açıklama |
|---|---|
| `HAYALAI_CSV` | Veri setini indirmek yerine bu yoldaki CSV dosyasını kullanır. |
| `XDG_CACHE_HOME` | Önbellek klasörünün konumu. Varsayılan `~/.cache`. |

## Geliştirme

```bash
npm test
```

Testler CSV ayrıştırıcıyı ve aramayı birim olarak, sunucuyu ise gerçek bir MCP istemcisiyle uçtan uca çalıştırır. Gerçek veri seti kullandıkları için ilk çalıştırmada indirme yapılır.

## Lisans

Sunucu kodu MIT lisanslıdır, bkz. [LICENSE](LICENSE). Promptların kaynakları ve lisansları [hayalai/LISANS-KAYNAKLAR.md](https://github.com/sercanesiktas/hayalai/blob/main/LISANS-KAYNAKLAR.md) dosyasında.
