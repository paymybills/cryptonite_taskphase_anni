### Challenge Overview

The MMORPG "All Alone in the Forest" e-sports tournament faced a controversy where 20 players exploited a glitch to overflow their inventories and achieve unrealistically low ping, gaining unfair advantages. The objective was to identify the cheating players and reconstruct their profile pictures to uncover the flag.

---

### Initial Approach

The dataset `datasetALLALONE.csv` contained columns such as:

- `PlayerID`, `GameSession`, `PlayerScore`, `ItemsCollected`, `ConnectionPing`, and more.
- The column `ProfilePic (256x256)` contained pixel arrays representing player profile pictures.

A basic AI model was built to flag suspicious players based on outliers in features like `ItemsCollected`, `ConnectionPing`, and `K/D Ratio`. Players were flagged if:
- `ItemsCollected > 95th percentile`
- `ConnectionPing < 5`

Additionally:
```python
df['K/D_Ratio'] = df['NumKills'] / (df['NumDeaths'] + 1e-5)
df['Efficiency'] = df['PlayerScore'] / (df['SessionDuration'] + 1e-5)
```
Flagged players were visualized, and some showed abnormal behavior. However, the real insight came from analyzing the `ProfilePic` column.

---

### Key Insight: Pixel Array Size

The `ProfilePic` column contained pixel arrays for player profile pictures. By filtering arrays with 65,536 elements (256x256 pixels), I isolated cheating players since their profiles uniquely met this condition.

---

### Step-by-Step Solution

#### 1. **Filter Pixel Arrays of Size 65,536**
Players with profile picture arrays of size 65,536 were filtered:
```python
import pandas as pd
import ast

# Load dataset
df = pd.read_csv("datasetALLALONE.csv")

# Filter players with 256x256 profile pictures
filtered_players = []
for _, row in df.iterrows():
    try:
        pixels = ast.literal_eval(row['ProfilePic (256x256)'])
        if len(pixels) == 256 * 256:
            filtered_players.append(row)
    except:
        pass

filtered_df = pd.DataFrame(filtered_players)
filtered_df.to_csv("filtered_players.csv", index=False)
```

#### 2. **Reconstruct Profile Pictures**
The filtered players’ profile pictures were reconstructed into images:
```python
from PIL import Image
import numpy as np
import ast

# Reconstruct images
for _, row in filtered_df.iterrows():
    pixels = np.array(ast.literal_eval(row['ProfilePic (256x256)']), dtype=np.uint8)
    image = Image.fromarray(pixels.reshape(256, 256, 3), 'RGB')
    image.save(f"profile_{row['PlayerID']}.png")
```

#### 3. **Handle Missing Images**
For profile pictures with RGBA channels:
```python
# Reconstruct RGBA images
pixels = np.array(ast.literal_eval(row['ProfilePic (256x256)']), dtype=np.uint8)
image = Image.fromarray(pixels.reshape(256, 256, 4), 'RGBA')
image.save(f"profile_{row['PlayerID']}_RGBA.png")
```

#### 4. **Sort Players by Score**
To organize the images based on player performance:
```python
sorted_df = filtered_df.sort_values(by=['PlayerScore'], ascending=False)
```

---

### Final Outcome

- **Cheating Players Identified**: 20 players were flagged by filtering pixel arrays of size 65,536.
- **Reconstructed Profile Pictures**: The images revealed letters forming the flag.
- **Flag**: `nite{4_R34L_0DD84LL}`

---
