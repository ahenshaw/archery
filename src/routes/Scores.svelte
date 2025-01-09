<script lang="ts">
    let { arrows } = $props();
    let rounds = extract_rounds(arrows);
    function extract_rounds(arrows: string) {
        let rounds = [];
        for (let round_index = 0; round_index < 2; round_index++) {
            let end_totals = [];
            let round_total = 0;
            let ends = [];
            let shot_count = 0;
            for (let end_index = 0; end_index < 10; end_index++) {
                let end_total = 0;
                let end = [];
                let flag = false;
                for (let arrow_index = 0; arrow_index < 3; arrow_index++) {
                    let index = 3*(round_index * 10 + end_index) + arrow_index;
                    let arrow = arrows.charAt(index);
                    if (arrow) {
                        end.push(arrow);
                        flag = true;
                        if (arrow == 'T') {end_total += 10;}
                        else if (arrow == 'M') {}
                        else {end_total +=  Number(arrow)}
                        shot_count += 1;
                    } else {
                        end.push("-")
                    }
                }
                if (flag) {
                    end_totals.push(end_total);
                    ends.push(end);
                } else {
                    end_totals.push("-");
                    ends.push(["-","-","-"]);
                }
                round_total += end_total;
            }
            end_totals.push(round_total);
            if (shot_count != 0){
                end_totals.push((round_total/shot_count).toFixed(2));
            }
            else {end_totals.push("-")}
            rounds.push([ends, end_totals])
        }
        return rounds;
    }
</script>

<table class="details">
    <tbody>
        <tr class="round">
            <td colspan="5">
                <table>
                    <tbody>
                        {#each rounds as round, index}
                        {@const row = index + 1}
                        {@const ends = round[0]}
                        {@const totals = round[1]}
                        <tr>
                            <th rowspan="2" class="round">{row}</th>
                            {#each ends as end}
                                <td class="arrows">
                                    {#each end as arrow}
                                        {#if arrow == "9"}
                                            <span class="nine">{arrow}</span>
                                        {:else if arrow == "T"}
                                            <span class="ten">{arrow}</span>
                                        {:else}
                                            <span class="default">{arrow}</span>
                                        {/if}
                                    {/each}
                                </td>
                            {/each}
                            <td class="arrows">Total</td>
                            <td class="arrows">Avg</td>
                        </tr>
                        <tr class="ends">
                            {#each totals as end_total}
                            <td class="end_total">{end_total}</td>
                            {/each}
                        </tr>
                        {#if index < rounds.length-1}
                        <tr class="gap"><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr>
                        {/if}
                        {/each}
                    </tbody>
                </table>
            </td>
        </tr>
    </tbody>
</table>

<!-- <table class="details">
    <tbody>
        <tr class="round">
            <td colspan="5">
                <table>
                    <tbody>
                        <tr>
                            <th rowspan="2" class="round">1</th>
                            <td class="arrows">8 2 M</td>
                            <td class="arrows">5 1 M</td>
                            <td class="arrows">5 M M</td>
                            <td class="arrows"><span class="nine">9</span> 7 3</td>
                            <td class="arrows">6 5 2</td>
                            <td class="arrows">7 4 M</td>
                            <td class="arrows">7 7 1</td>
                            <td class="arrows">8 5 M</td>
                            <td class="arrows">7 3 M</td>
                            <td class="arrows">7 6 4</td>
                            <td class="arrows">Total</td>
                            <td class="arrows">Avg</td>
                        </tr>
                        <tr class="ends">
                            <td class="end_total">10</td>
                            <td class="end_total">6</td>
                            <td class="end_total">5</td>
                            <td class="end_total">19</td>
                            <td class="end_total">13</td>
                            <td class="end_total">11</td>
                            <td class="end_total">15</td>
                            <td class="end_total">13</td>
                            <td class="end_total">10</td>
                            <td class="end_total">17</td>
                            <td class="end_total">119</td>
                            <td class="end_total">4.0</td>
                        </tr>
                        <tr class="gap"><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr>
                        <tr>
                            <th rowspan="2" class="round">2</th>
                            <td class="arrows">7 6 5</td>
                            <td class="arrows"><span class="nine">9</span> 8 5</td>
                            <td class="arrows">8 7 2</td>
                            <td class="arrows">8 7 6</td>
                            <td class="arrows">4 4 M</td>
                            <td class="arrows"><span class="nine">9</span> 8 5</td>
                            <td class="arrows"><span class="nine">9</span> 7 6</td>
                            <td class="arrows"><span class="ten">10</span> 5 4</td>
                            <td class="arrows">5 4 2</td>
                            <td class="arrows">6 4 3</td>
                            <td class="arrows">Total</td>
                            <td class="arrows">Avg</td>
                        </tr>
                        <tr class="ends">
                            <td class="end_total">18</td>
                            <td class="end_total">22</td>
                            <td class="end_total">17</td>
                            <td class="end_total">21</td>
                            <td class="end_total">8</td>
                            <td class="end_total">22</td>
                            <td class="end_total">22</td>
                            <td class="end_total">19</td>
                            <td class="end_total">11</td>
                            <td class="end_total">13</td>
                            <td class="end_total">173</td>
                            <td class="end_total">5.8</td>
                        </tr>
                    </tbody>
                </table>
            </td>
        </tr>
    </tbody>
</table> -->
